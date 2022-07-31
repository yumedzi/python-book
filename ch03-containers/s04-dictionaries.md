# Dictionaries

> Dictionary is mutable mapping type (also know as hash or key-value collection).

In other words it's structure of key-value elements. Keys can be only hashable objects (all *immutable objects* and *instances* of classes). Values can be of any type.

Keys/values elements are unordered (their position in memory is based on result of ```hash()``` function used on a key.

Ways to create a dictionary:
* ```{}```
* ```dict()```
* ```{"name": "John", "surname": "Snow"}```
* ```dict(name="John", surname="Snow")```

Result of `dict(some_dict)` will be shallow copy of `some_dict`

We can create a copy with some new keys:


```python
d = {"name": "John", "surname": "Snow"}
new_d = dict(d, profession="Bastard")
new_d
```




    {'name': 'John', 'surname': 'Snow', 'profession': 'Bastard'}



We can even rewrite some old key-values:


```python
new_d = dict(d, surname="Stark")
new_d
```




    {'name': 'John', 'surname': 'Stark'}



And also we can create a dict from an iterable with pair key-value


```python
d1 = dict([("Aria", "Stark"), ("Faceless", "Man")])
print("d1:", d1)
pairs = ["Yaken Gharr".split(), "Sirio Forell".split()]
d2 = dict(pairs)
print("d2:", d2)
```

    d1: {'Aria': 'Stark', 'Faceless': 'Man'}
    d2: {'Yaken': 'Gharr', 'Sirio': 'Forell'}


Using method `dict.fromkeys` we can create a new dict from an iterable (some collection) of keys.
Second attribute will allow to set a default value for all keys (or it will be `None`).


```python
dict.fromkeys(["name", "surname"])
```




    {'name': None, 'surname': None}




```python
dict.fromkeys(["John", "Bob", "Brandon"], "Stark")
```




    {'John': 'Stark', 'Bob': 'Stark', 'Brandon': 'Stark'}



It is recommended to pass some immutable object as the default value. Otherwise you could get unexpected results:


```python
d = dict.fromkeys("abcde", [])
d
```




    {'a': [], 'b': [], 'c': [], 'd': [], 'e': []}




```python
d["a"].append(1)
d 
```




    {'a': [1], 'b': [1], 'c': [1], 'd': [1], 'e': [1]}



There are (from 3.5) even more craziest ways of dict creation:


```python
d1 = {"some_key": "some_value"}
d2 = {**d1} 
d1 is d2, d2
```




    (False, {'some_key': 'some_value'})




```python
defaults = {"John": "Snow", "Aria": "Stark"}
new_book = {**defaults, "John": "Stark"}
print(new_book)
```

    {'John': 'Stark', 'Aria': 'Stark'}


## How dictionaries work

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Dictionary lookup is done in three steps:

1. A hash value of the key is computed using a hash function.
    * hash functions provided must guarantee that if two keys produce different hash values then the two key objects are not equivalent
    * that's why `objectA == objectB` it's also needed that `hash(objectA) == hash(objectB)`

2. The hash value addresses a location in d.data which is
  supposed to be an array of "buckets" or "collision lists"
  which contain the (key,value) pairs.

3. The collision list addressed by the hash value is searched
  sequentially until a pair is found with `pair[0] == key`. The
  return value of the lookup is then `pair[1]`.


<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

```python
def lookup(d, key):
    "Find a key `key` in a dict `d`"
    h = hash(key)                  # step 1
    cl = d.data[h]                 # step 2
    for pair in cl:                # step 3
        if key == pair[0]:
            return pair[1]
    else:
        raise KeyError, "Key %s not found." % key
```

<span title="Advanced topic" style="position: absolute; top: 5px; right: 30px; font-size: 250%; color:red">🔥</span>

<span style="margin-bottom:100px">&nbsp;</span>

That's why for dictionaries keys we can use only those objects that support hash function (e.g. through `__hash__`), equality comparison (e.g. through `__eq__` or `__cmp__`), and must satisfy the correctness condition above.

And that's why mutable objects (like lists) can't have `__hash__()` - even if we base on `id()` we just can't guarantee that two lists won't be equal in future.

On the contrary, by default, all user defined types (instances of `class`) are usable as dictionary keys with `hash(object)` defaulting to `id(object)`.



## Main methods of dictionaries


```python
some_dict = {"name": "John", "surname": "Snow"}
print( dir(some_dict) ) # All methods a gain
```

    ['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']


#### Dictionary methods

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```len()```     | Return a number of keys in dictionary
| ```some_dict[x]```     | Return (or assign) value for key ```x```
| ```get(x, d)```        | Return value for key ```x``` or ```d``` if it is not found
| ```x in some_dict```   | Return True/False - is key ```x``` is in dictionary?
| ```keys()```    | Return a *view* object that provides an access to all keys in dictionary
| ```values()```  | Return a *view* object that provides an access to all values in dictionary 
| ```items()```   | Return a *view* object that provides an access to all `(key, value)` pairs
| ```del some_dict[key]```| Remove element by key from dictionary 

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```pop(k, d)```         | Return value and remove key from dictionary (```d``` - default value)
| ```popitem()```         | Return tuple ```(key, value)``` and remove it from dictionary
| ```update(other_dict)```          | Update dictionary with key-values of ```other_dict```
| ```update(x1=y1, x2=y2, ...)```   | Update dictionary with key-values pairs: "x1": "y1", "x2": "y2", ...
| ```clear()```                     | Empty whole dictionary (the same as ```some_dict = {}```
| ```copy()```                      | Return shallow copy of dictionary
| ```setdefault(k, d)```            | Set value ```d``` for key ```k``` is it was not found and/or return value for that key

## Examples


```python
some_dict["name"]
```




    'John'




```python
some_dict["surname"] = "Stark"
some_dict
```




    {'name': 'John', 'surname': 'Stark'}




```python
some_dict["alive"] = True
some_dict
```




    {'name': 'John', 'surname': 'Stark', 'alive': True}



### Method `get`

Trying to obtain unexistent key will be resulted in ```KeyError``` exception


```python
some_dict["6th_book"]
```


    

    KeyErrorTraceback (most recent call last)

    <ipython-input-69-9dbfbd76b8e1> in <module>()
    ----> 1 some_dict["6th_book"]
    

    KeyError: '6th_book'


More correctly:


```python
if "6th_book" in some_dict:
    print(some_dict["6th_book"])
else:
    print("Martin!....:(")
```

    Martin!....:(


Even better - use ```get()```

> Using `get` is very "pythonic"

1. Shorter!
2. Only 1 (instead of 2) requests to dict
3. Can specify a default value


```python
some_dict.get("6th_book", "Nope....")
```




    'Nope....'



### Method `setdefault`

This method allows to write a "default" value for specific key and/or return set or that default value. In other words it will update dictionary only when the key is not found in it.


```python
d = {"John": "Snow"}
d.setdefault("John", "Stark")
d.setdefault("Aria", "Stark")
d
```




    {'John': 'Snow', 'Aria': 'Stark'}



So, the code:


```python
print(d.setdefault("Robert", "Baration"))
```

    Baration


is the same as:


```python
if "Robert" not in d:
    d["Robert"] = "Baration"
print(d["Robert"])
```

    Baration


If the default value is a list it can used for appending the needed value right away:


```python
characters = "aaaasddfgsadfgdsadfsa" 

def counter(str_):
    dict_ = {}
    for char in str_:
        dict_.setdefault(char, str_.count(char))
    return dict_
    
print(counter(characters))
```

    {'a': 7, 's': 4, 'd': 5, 'f': 3, 'g': 2}


### Method `update`

Doc says:
```python
D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
In either case, this is followed by: for k in F:  D[k] = F[k]
```

The same syntax can be used with `dict()`.


```python
d = {}
d.update(a=1, b=2)
d
```




    {'a': 1, 'b': 2}




```python
d = {}
d.update([("a", 1), ("b", 2)])
d
```




    {'a': 1, 'b': 2}



And crazy example - two syntaxes altogether:


```python
d = {}
d.update([("Aria", "Stark"), ("Yaken", "Gharr")], Faceless="Man", some_other_key=123)
d
```




    {'Aria': 'Stark', 'Yaken': 'Gharr', 'Faceless': 'Man', 'some_other_key': 123}



### Deleting

Regular `del` here too:


```python
del d["Yaken"]
d
```




    {'Aria': 'Stark', 'Faceless': 'Man', 'some_other_key': 123}



To clear all keys it is possible to use `clear()`


```python
d.clear()
d
```




    {}



Also - just like with lists we have `pop()` and `popitem()` methods.

* `pop(k [,v])` will return value by key `k` or default value `d`
* `popitem()` will return last added pair (from Python 3.6) OR some random pair (before Python 3.6) `(key, value)` and raise `KeyError` if dict is empty


```python
d = {'Aria': 'Stark', 'Faceless': 'Man', 'Yaken': 'Gharr', 'some_other_key': 123}
print(d.pop("Faceless"))
print("What is left:", d)
print(d.popitem())
print("What is left:", d)
```

    Man
    What is left: {'Aria': 'Stark', 'Yaken': 'Gharr', 'some_other_key': 123}
    ('some_other_key', 123)
    What is left: {'Aria': 'Stark', 'Yaken': 'Gharr'}


### Dictionary view objects

The methods `dict.keys()`, `dict.values()` and `dict.items()` return so-called `view` objects in Python 3 (in Python 2 they return a list of corresponding values - all keys, all values and all key-value pairs). 

*View* objects provide a *dynamic view* on the dictionary's data, which means that when the dictionary changes, the view reflects these changes right away. 

Changes per versions:
* `3.7`: Dictionary order is guaranteed to be insertion order.
* `3.8`: Dictionary views are now reversible.

Dictionary views can be iterated over to yield their respective data, support membership tests and basic `set`-like operations like `&` and `|` (which is `union` and `intersection`):

* `len(dictview)`
    * Return the number of entries in the dictionary.
* `iter(dictview)`
    * Return an iterator over the keys, values or items (represented as tuples of (key, value)) in the dictionary.
* `x in dictview`
    * Return True if x is in the underlying dictionary’s keys, values or items (in the latter case, x should be a (key, value) tuple).
* `reversed(dictview)`
    * Return a reverse iterator over the keys, values or items of the dictionary. The view will be iterated in reverse order of the insertion.

Some examples of usage `dictviews` objects:


```python
d = {'Alfa': 0, 'Bravo': 1, 'Charlie': 2, 'Delta': 3}
print(f'dict is {d}', end="\n - - -\n")

keys, values = d.keys(), d.values()

print(f"keys (len is {keys}): {keys}")
print("list(keys):", list(keys), end="\n - - -\n")

print(f"values:  (len is {len(values)}): {values}")
print("list(values):", list(values))
```

    dict is {'Alfa': 0, 'Bravo': 1, 'Charlie': 2, 'Delta': 3}
     - - -
    keys (len is dict_keys(['Alfa', 'Bravo', 'Charlie', 'Delta'])): dict_keys(['Alfa', 'Bravo', 'Charlie', 'Delta'])
    list(keys): ['Alfa', 'Bravo', 'Charlie', 'Delta']
     - - -
    values:  (len is 4): dict_values([0, 1, 2, 3])
    list(values): [0, 1, 2, 3]


Check how dynamic are `dictviews`:


```python
print("Before:", d.keys())

del d['Charlie']
del d['Delta']

print("After:", d.keys())
```

    Before: dict_keys(['Alfa', 'Bravo', 'Charlie', 'Delta'])
    After: dict_keys(['Alfa', 'Bravo'])


## Dictionary comprehesions


```python
{x:1 for x in range(5)}  
```




    {0: 1, 1: 1, 2: 1, 3: 1, 4: 1}



Not so oftenly used because:


```python
{x:y for x in range(3) for y in range (3)} 
```




    {0: 2, 1: 2, 2: 2}



Sometimes dictionary comprehension is useful when you need to set a default mutable value (so `dict.fromkeys` is not good)


```python
d = {x:[] for x in "abcde"}
d["a"].append(1)
d
```




    {'a': [1], 'b': [], 'c': [], 'd': [], 'e': []}



## Complexity of operations

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

|Operation |Average Case|Amortized Worst Case |
|------------|------------|----------------------------|
|Copy |O(n) |O(n) |
|Get Item |O(1) |O(n) |
|Set Item[1] |O(1) |O(n) |
|Delete Item |O(1) |O(n) |
|Iteration |O(n) |O(n) |