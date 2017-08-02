# Dictionaries

> Dictionary is mutable mapping type (also know as hash or key-value collection).

In other words it's structure of key-value elements. Keys can be only hashable objects (all immutable objects and instances of classes). Values can be of any type.

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
Output:



    {'name': 'John', 'profession': 'Bastard', 'surname': 'Snow'}



We can even rewrite some old key-values:


```python
new_d = dict(d, surname="Stark")
new_d
```

Output:


    {'name': 'John', 'surname': 'Stark'}



And also we can create a dict from an iterable with pair key-value


```python
d1 = dict([("Aria", "Stark"), ("Faceless", "Man")])
print("d1:", d1)
pairs = ["Yaken Gharr".split(), "Sirio Forell".split()]
d2 = dict(pairs)
print("d2:", d2)
```
Output:

    d1: {'Aria': 'Stark', 'Faceless': 'Man'}
    d2: {'Sirio': 'Forell', 'Yaken': 'Gharr'}
    

Using method `dict.fromkeys` we can create a new dict from an iterable (some collection) of keys.
Second attribute will allow to set a default value for all keys (or it will be `None`).


```python
>>> dict.fromkeys(["name", "surname"])
{'name': None, 'surname': None}

>>> dict.fromkeys(["John", "Bob", "Brandon"], "Stark")
{'Bob': 'Stark', 'Brandon': 'Stark', 'John': 'Stark'}
```

It is recommended to pass some immutable object as the default value. Otherwise you could get unexpected results:


```python
>>> d = dict.fromkeys("abcde", [])
>>> d
{'a': [], 'b': [], 'c': [], 'd': [], 'e': []}

>>> d["a"].append(1)
>>> d 
{'a': [1], 'b': [1], 'c': [1], 'd': [1], 'e': [1]}
```

There are (from 3.5) even more craziest ways of dict creation:


```python
>>> d1 = {"some_key": "some_value"}
>>> {**d1}
{'some_key': 'some_value'}

>>> defaults = {"John": "Snow", "Aria": "Stark"}
>>> new_book = {**defaults, "John": "Stark"}
>>> new_book
{'John': 'Stark', 'Aria': 'Stark'}
```

## How dictionaries work

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


```python
def lookup(d, key):
    h = hash(key)                  # step 1
    cl = d.data[h]                 # step 2
    for pair in cl:                # step 3
        if key == pair[0]:
            return pair[1]
    else:
        raise KeyError, "Key %s not found." % key
```

That's why for dictionaries keys we can use only those objects that support hash function (e.g. through `__hash__`), equality comparison (e.g. through `__eq__` or `__cmp__`), and must satisfy the correctness condition above.

And that's why mutable objects (like lists) can't have `__hash__()` - even if we base on `id()` we just can't guarantee that two lists won't be equal in future.

On the contrary, by default, all user defined types (instances of `class`) are usable as dictionary keys with `hash(object)` defaulting to `id(object)`.



## Main methods of dictionaries


```python
some_dict = {"name": "John", "surname": "Snow"}
print( dir(some_dict) ) # All methods again
```
Output:

    ['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', 
    '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', 
    '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', 
    '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 
    'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 
    'update', 'values']
    

## Dictionary methods

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```len()```     | Return a number of keys in dictionary
| ```some_dict[x]```     | Return (or assign) value for key ```x```
| ```get(x, d)```        | Return value for key ```x``` or ```d``` if it is not found
| ```x in some_dict```   | Return True/False - is key ```x``` is in dictionary?
| ```keys()```    | Return a list iterator with all keys in dictionary
| ```values()```  | Return a list iterator with values for all keys in dictionary 
| ```items()```   | Return a list with tuple (key, value)
| ```del some_dict['x']```| Remove element by key from dictionary 
| ```pop(k, d)```         | Return value and remove key from dictionary (```d``` - default value)
| ```popitem()```         | Return tuple ```(key, value)``` and remove it from dictionary
| ```update(other_dict)```          | Update dictionary with key-values of ```other_dict```
| ```update(x1=y1, x2=y2, ...)```   | Update dictionary with key-values pairs: "x1": "y1", "x2": "y2", ...
| ```clear()```                     | Empty whole dictionary (the same as ```some_dict = {}```
| ```copy()```                      | Return shallow copy of dictionary
| ```setdefault(k, d)```            | Set value ```d``` for key ```k``` is it was not found and/or return value for that key

## Examples


```python
>>> some_dict["name"]
'John'

>>> some_dict["surname"] = "Stark"
>>> some_dict
{'name': 'John', 'surname': 'Stark'}

>>> some_dict["alive"] = True
>>> some_dict
{'alive': True, 'name': 'John', 'surname': 'Stark'}
```


## Method `get`

Trying to obtain unexistent key will be resulted in ```KeyError``` exception


```python
some_dict["6th_book"]
```
Output:

    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-112-89352f47a745> in <module>()
    ----> 1 some_dict["6th_book"]
    

    KeyError: '6th_book'


This can be avoided by checking if this key exists:

```python
if "6th_book" in some_dict:
    print(some_dict["6th_book"])
else:
    print("Martin! Y no book yet? :(")
```
Output:

    Martin! Y no book yet? :(
    

But it is recommended to use ```get()``` method

Using `get` is very "pythonic" because:

1. It is shorter than version with condition or `try`/`except`!
2. Only 1 (instead of 2) requests to dict
3. Can specify a default value


```python
>>> some_dict.get("6th_book", "Nope....")  # "Nope...." is default value here
'Nope....'
```

## Method `setdefault`

This method allows to write a "default" value for specific key. In other words it will update dictionary only when the key is not found in it.


```python
>>> d = {"John": "Snow"}
>>> d.setdefault("John", "Stark")
>>> d.setdefault("Aria", "Stark")
>>> d
{'Aria': 'Stark', 'John': 'Snow'}
```

## Method `update`

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

Output:


    {'a': 1, 'b': 2}




```python
d = {}
d.update([("a", 1), ("b", 2)])
d
```

Output:


    {'a': 1, 'b': 2}



And crazy example - two syntaxes altogether:


```python
d = {}
d.update([("Aria", "Stark"), ("Yaken", "Gharr")], Faceless="Man", some_other_key=123)
d
```

Output:


    {'Aria': 'Stark', 'Faceless': 'Man', 'Yaken': 'Gharr', 'some_other_key': 123}



## Deleting

Regular `del` here too:


```python
del d["Yaken"]
d
```

Output:


    {'Aria': 'Stark', 'Faceless': 'Man', 'some_other_key': 123}



To clear all keys it is possible to use `clear()`


```python
d.clear()
d
```

Output:

    {}



Also - just like with lists we have `pop()` and `popitem()` methods.

* `pop(k [,v])` will return value by key `k` or default value `d`
* `popitem()` will return some random pair `(key, value)` and raise `KeyError` if dict is empty


```python
d = {'Aria': 'Stark', 'Faceless': 'Man', 'Yaken': 'Gharr', 'some_other_key': 123}
print(d.pop("Faceless"))
print("What is left:", d)
print(d.popitem())
print("What is left:", d)
```
Output:

    Man
    What is left: {'Aria': 'Stark', 'some_other_key': 123, 'Yaken': 'Gharr'}
    ('Aria', 'Stark')
    What is left: {'some_other_key': 123, 'Yaken': 'Gharr'}
    

## Dictionary comprehesions


```python
>>> {x:1 for x in range(5)} 
{0: 1, 1: 1, 2: 1, 3: 1, 4: 1}
```

Not so oftenly used because:


```python
>>> {x:y for x in range(3) for y in range (3)}
{0: 2, 1: 2, 2: 2} 
```

Sometimes dictionary comprehension is useful when you need to set a default mutable value (so `dict.fromkeys` is not good)


```python
d = {x:[] for x in "abcde"}
d["a"].append(1)
d
```
Output:

    {'a': [1], 'b': [], 'c': [], 'd': [], 'e': []}


## Complexity of operations

|Operation |Average Case|Amortized Worst Case |
|------------|------------|----------------------------|
|Copy |O(n) |O(n) |
|Get Item |O(1) |O(n) |
|Set Item[1] |O(1) |O(n) |
|Delete Item |O(1) |O(n) |
|Iteration |O(n) |O(n) |