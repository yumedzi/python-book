# Lists

> List is ordered mutable sequence of ANY objects.

> This means that it is allowed to change it's elements after creation: adding new, changing/removing existing etc.

Ways to create a list:
* ```[]```
* ```list()```
* ```[1, 2, 3, [10, 20], 5]```

### Main methods


🪄 <mark style="color:red;">Code</mark>:

```python
some_list = [4, 8, 15, 16, 23, 42]
print(dir(some_list))  # Again all methods
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['__add__', '__class__', '__class_getitem__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```
{% endcode %}
Actually beside magical methods (containing \_\_) there are not so much methods left

Worth to note that most methods are not returning anything - they are just directly changing the list itself because it is mutable object.

#### List methods

| Method(s)               |  Description                                                                              |
|-------------------------|-----------------------------------------------------------------------------------------
| ```len(some_list)```       | Return int - length of the list
| ```reverse()```            | Reverse order of elements of the list in place
| ```sort()```               | Sort elements of the list in place
| ```append(x)```            | Add new element ```x``` to the end of the list
| ```extend(iterable)```     | Append elements of iterable to the end of the list
| ```pop()```                | Return and remove the last element from the list
| ```pop(i)```               | Return and remove element by index ```i``` from the list

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```some_list[i]```      | Return (or assign) element by index ```i``` (int)
| ```some_list[i:j]```    | Return new list - slice from element by index ```i``` till ```j-1```
| ```some_list[i:j:z]```  | Return new list - slice with step ```z```
| ```del some_list[3]```     | Remove element of index ```3``` from list ```some_list```
| ```del some_list[2:4]```   | Remove part (starting from index ```2``` till ```3```) from list ```some_list```
| ```2 in some_list```    | Return True/False - is object ```2```is part of list ```some_list```?
| ```some_list + ["a", "b"]``` | Return new list - a sum of merged lists


| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```count(x)```    | Return number of object ```x``` found in a list
| ```index(x)```    | Return first index of object ```x``` in list or raise ```ValueError``` exception if not found

Last two we saw in strings as well.


## Examples

Lists are indexable, starting at 0


🪄 <mark style="color:red;">Code</mark>:

```python
print(some_list)
print(some_list[0])
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
4
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[2]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
15
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[-1]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
42
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
print(some_list)
print(len(some_list))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
6
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list.reverse()
print(some_list)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[42, 23, 16, 15, 8, 4]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list.sort()
print(some_list)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
new_list = some_list + ["a", "b", "c"]
print(new_list)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42, 'a', 'b', 'c']
```
{% endcode %}
### Sorting

> Sorting of the list with elements of different types in Python 3 is forbidden (yields an TypeError exception about unsupported `<` operation).


🪄 <mark style="color:red;">Code</mark>:

```python
new_list 
new_list.sort()
```


📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

Input In [282], in <cell line: 2>()
      1 new_list 
----> 2 new_list.sort()


TypeError: '<' not supported between instances of 'str' and 'int'
```
{% endcode %}
But we can workaround this by specifying your own sorting function (as argument `key`) which should return some values of the same type which Python will be sorting instead of real values.


🪄 <mark style="color:red;">Code</mark>:

```python
new_list.sort(key=str) # Here we are sorting in fact by string representations
print(new_list)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 23, 4, 42, 8, 'a', 'b', 'c']
```
{% endcode %}
### Appending, extending


🪄 <mark style="color:red;">Code</mark>:

```python
some_list.append(1000)
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42, 1000]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list = [4, 8, 15, 16, 23, 42, 1000]
some_list.extend([1000, [10, 10, [20, 20]], some_list])
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42, 1000, 1000, [10, 10, [20, 20]], [...]]
```
{% endcode %}
By extending nested list Python will treat all nested as elements just as other types


🪄 <mark style="color:red;">Code</mark>:

```python
some_list.extend([ 0, [1,2], [3, 4]])
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[4,
 8,
 15,
 16,
 23,
 42,
 1000,
 1000,
 [10, 10, [20, 20]],
 [...],
 0,
 [1, 2],
 [3, 4]]
```
{% endcode %}
### Removing


🪄 <mark style="color:red;">Code</mark>:

```python
some_list.pop()
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[3, 4]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list.pop(0)
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
4
```
{% endcode %}
```python
del some_list[0]
del some_list[3:6]
```


🪄 <mark style="color:red;">Code</mark>:

```python
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]
```
{% endcode %}
### Other examples
We saw very similar examples for strings - because strings are sequence too. That is the core idea (called ducktyping) in Python - the same behavior even if the types are different.


🪄 <mark style="color:red;">Code</mark>:

```python
some_list * 2
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15,
 16,
 23,
 [10, 10, [20, 20]],
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 0,
 [1, 2],
 15,
 16,
 23,
 [10, 10, [20, 20]],
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 0,
 [1, 2]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[::-1]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[[1, 2],
 0,
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 [10, 10, [20, 20]],
 23,
 16,
 15]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[:4]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 23, [10, 10, [20, 20]]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[2:]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[23,
 [10, 10, [20, 20]],
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 0,
 [1, 2]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
print (some_list)
some_list[-2]
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]





0
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
(some_list * 4)[::4]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15,
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 16,
 0,
 23,
 [1, 2],
 [10, 10, [20, 20]]]
```
{% endcode %}
```IndexError``` exception is raised for non-existent index element


🪄 <mark style="color:red;">Code</mark>:

```python
some_list[1000]
```


📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
---------------------------------------------------------------------------

IndexError                                Traceback (most recent call last)

Input In [297], in <cell line: 1>()
----> 1 some_list[1000]


IndexError: list index out of range
```
{% endcode %}
## List slices

Slices of list object are a bit different to the slices of strings due to the fact that lists are mutable. Because of these additional operations are available:

* slice deletion
* slice assignment

Firstly, let's check regular list slice obtaining:

### Slice obtaining


🪄 <mark style="color:red;">Code</mark>:

```python
print (some_list)
some_list[2:4]
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]





[23, [10, 10, [20, 20]]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[2:4] = ["a", "b", "c"]
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[15, 16, 'a', 'b', 'c', [...], 0, [1, 2]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
some_list[:1] = [100, 100, 100]
some_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[100, 100, 100, 16, 'a', 'b', 'c', [...], 0, [1, 2]]
```
{% endcode %}
### Slice deletion

By using `del` operator on the slice it is possible to delete target part from the original list:


🪄 <mark style="color:red;">Code</mark>:

```python
list_ = list(range(1, 6))
print("Before:", list_)

del list_[2:4]
print("After:", list_)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Before: [1, 2, 3, 4, 5]
After: [1, 2, 5]
```
{% endcode %}
### Slice assignment

By assignining the slice to another iterable, the content of that iterable will be used to replace the target part of the original list:


🪄 <mark style="color:red;">Code</mark>:

```python
list_ = list(range(1, 6))
print("Before:", list_)

list_[2:4] = ["A"]
print("After:", list_)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Before: [1, 2, 3, 4, 5]
After: [1, 2, 'A', 5]
```
{% endcode %}
## List comprehensions

> Fast, simple and "Pythonic" way to create a list

Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition


🪄 <mark style="color:red;">Code</mark>:

```python
cool_list = [x*2 for x in range(10)]
cool_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
{% endcode %}
It's absolutely the same as:


🪄 <mark style="color:red;">Code</mark>:

```python
cool_list = []
for x in range(10):
    cool_list.append(x*2)
cool_list
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
[x**2 + 2*x + 1 for x in range(10)]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
# Random list (len till 15) from rand ints (till 10)
from random import randrange
[randrange(0, 10) for _ in range(randrange(3, 15))]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[9, 2, 2, 4, 6, 2]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
[f"{x}-{y}" for x in [1, 2, 3] for y in "ABC"]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['1-A', '1-B', '1-C', '2-A', '2-B', '2-C', '3-A', '3-B', '3-C']
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
list_ = []
for x in [1, 2, 3]:
    for y in "ABC":
        list_.append(f"{x}-{y}")
print(list_)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['1-A', '1-B', '1-C', '2-A', '2-B', '2-C', '3-A', '3-B', '3-C']
```
{% endcode %}
The order of loops matters:


🪄 <mark style="color:red;">Code</mark>:

```python
[f'{x}-{y}' for x in "abc" for y in range(1, 4)]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['a-1', 'a-2', 'a-3', 'b-1', 'b-2', 'b-3', 'c-1', 'c-2', 'c-3']
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
[f'{x}-{y}' for y in range(1, 4) for x in "abc"]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['a-1', 'b-1', 'c-1', 'a-2', 'b-2', 'c-2', 'a-3', 'b-3', 'c-3']
```
{% endcode %}
It's possible to create nested list and use conditions as well:


🪄 <mark style="color:red;">Code</mark>:

```python
[(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```
{% endcode %}
is equivalent to:


🪄 <mark style="color:red;">Code</mark>:

```python
combs = []
for x in [1, 2, 3]:
    for y in [3, 1, 4]:
        if x != y:
            combs.append((x, y))
combs
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```
{% endcode %}
Some "real-world" example:

```python
[func(x, y) for x in list_x for y in list_y if check(x, y)]
```

## Deep/shallow copy

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Variables in Python (name bindings) are just points to an object in memory. By assigning one variable to another we make them point to the same object which may lead to various problems.

Operator ```is``` allows comparing by ids - shows is two variables pointing to the same object 


🪄 <mark style="color:red;">Code</mark>:

```python
a = [1, 2, 3]
b = a
print (a is b)
a[0] = "Surprise"
print ("b is", b)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
True
b is ['Surprise', 2, 3]
```
{% endcode %}
### Shallow copy of lists

Create completely new copy of the list - by creating a new list and adding elements one by one from old one


🪄 <mark style="color:red;">Code</mark>:

```python
b = a.copy() # Pythonic way
b = list(a) # Almost Pythonic way
b = a[:] # hacker way

print (b is a)
a[0] = "Oh!"
print ("a is:", a)
print ("b is:", b)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
False
a is: ['Oh!', 2, 3]
b is: ['Surprise', 2, 3]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
b = a[:]  # Hackish way
a[0] = "New"
print ("b is:", b)
print(a)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
b is: ['Oh!', 2, 3]
['New', 2, 3]
```
{% endcode %}
### Shallow copy problems
If list has mutable object deeper than on the very first nesting level - shallow copy will cause similar problems as before.


🪄 <mark style="color:red;">Code</mark>:

```python
a = [[1, 2], 3]
b = list(a)
a[0][0] = "Surprise!"
print (a is b)
print ("b is:", b)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
False
b is: [['Surprise!', 2], 3]
```
{% endcode %}
### Deep copy

There is a special standard module for copying - ```copy```


🪄 <mark style="color:red;">Code</mark>:

```python
import copy
a = [[1, 2], 3]

# Shallow copy
b = copy.copy(a)

# Deep copy
c = copy.deepcopy(a)
a[0][0] = "Surprise!"
print ("b is:", b)
print ("c is:", c)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
b is: [['Surprise!', 2], 3]
c is: [[1, 2], 3]
```
{% endcode %}
### Self-referencing list

List is seqence-like object that contains pointers to other objects which are treated as it's elements.
That's why it's possible to add list to itself as element!


🪄 <mark style="color:red;">Code</mark>:

```python
a = [1, 2, 3]
a.append(a)
print(a)
print(a[-1][-1][-1][-1][-1][-1][-1])
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[1, 2, 3, [...]]
[1, 2, 3, [...]]
```
{% endcode %}
In this case when we ```del```ete it - Python garbage collector won't delete from memory - because the number of reference to this object is not null

Usual Python console:
    
🪄 <mark style="color:red;">Code</mark> <mark style="color:blue;">>>></mark> and <mark style="color:green;">📟</mark> <mark style="color:green;">Output</mark>:


```python
>>> a = [1, 2, 3]
>>> import sys
>>> sys.getrefcount(a)
2
>>> a.append(a)
>>> sys.getrefcount(a)
3
```


You need to be aware of such cases.

### Lists for heavy calculations

If you use list for complex math calculations - consider using `numpy`.

They are a bit slower to create:


🪄 <mark style="color:red;">Code</mark>:

```python
import numpy
array_ = numpy.array(list(range(1000)))
list_ = list((range(1000)))

%timeit 999 in list_
%timeit 999 in array_
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
15.3 µs ± 99.8 ns per loop (mean ± std. dev. of 7 runs, 100,000 loops each)
20.4 µs ± 373 ns per loop (mean ± std. dev. of 7 runs, 10,000 loops each)
```
{% endcode %}
But they are much faster (x5 in the following example) for a vector operations:


🪄 <mark style="color:red;">Code</mark>:

```python
import math

%timeit list(map(math.sqrt, list_))
%timeit numpy.sqrt(array_)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
109 µs ± 1.48 µs per loop (mean ± std. dev. of 7 runs, 10,000 loops each)
21.3 µs ± 317 ns per loop (mean ± std. dev. of 7 runs, 10,000 loops each)
```
{% endcode %}
## Complexity of operations

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Time-complexity (aka "Big O" or "Big Oh") of various operations in current CPython.

> Generally, 'n' is the number of elements currently in the container. 'k' is either the value of a parameter or the number of elements in the parameter.

|Operation |Average Case|Amortized Worst Case |
|------------|------------|----------------------------|
|Copy        |O(n) |O(n) |
|Append      |O(1) |O(1) |
|Insert      |O(n) |O(n) |
|Get Item    |O(1) |O(1) |
|Set Item    |O(1) |O(1) |
|Delete Item |O(n) |O(n) |

|Operation |Average Case|Amortized Worst Case |
|------------|------------|----------------------------|
|Iteration   |O(n) |O(n) |
|Get Slice   |O(k) |O(k) |
|Del Slice   |O(n) |O(n) |
|Set Slice   |O(k+n) |O(k+n) |
|Extend      |O(k) |O(k) |
|Sort        |O(n log n) |O(n log n) |
|Multiply    |O(nk) |O(nk) |
|x in s |O(n) | |
|min(s), max(s) |O(n) | |
|Get Length     |O(1) |O(1) |


As we can see from [Complexity of operations](#Complexity-of-operations) section, `list` has fast (complexity is `O(1)`) such methods as `append` and `pop` which work with right end of the structure. So this is a *FILO* structure - "stack". So, if we want to achieve maximum performance we should use list as stack (and not use `insert(0, x)` and `pop(0)` methods).