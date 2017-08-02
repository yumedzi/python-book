# Lists

> List is ordered mutable sequence of objects.

> This means that it is allowed to change it's elements after creation: adding new, changing/removing existing etc.

> Lists can contain any type of object.

Ways to create a list:
* ```[]```
* ```list()```
* ```[1, 2, 3, [10, 20], 5]```

### Main methods

```python
some_list = [4, 8, 15, 16, 23, 42]
print(dir(some_list)) # Again all methods
```
Output: 
```
    ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__',
    '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', 
    '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', 
    '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', 
    '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 
    'remove', 'reverse', 'sort']
```    

Actually beside magical methods (containing `__`) there are not so much methods left.

Worth to note that most methods are not returning anything - they are just directly changing the list itself because it is mutable object.

## List methods

| Method(s)               |  Description                                                                              |
|-------------------------|-----------------------------------------------------------------------------------------
| ```len(some_list)```     | Return int - length of the list
| ```reverse()```            | Reverse order of elements of the list
| ```sort()```               | Sort elements of the list
| ```append(x)```            | Add new element ```x``` to the end of list
| ```extend(another_list)``` | Add elements of list ```another_list``` to the end of list
| ```pop()```                | Return and remove the last element from the list
| ```pop(i)```               | Return and remove element by index ```i``` from the list
| ```some_list[i]```      | Return (or assign) element by index ```i``` (int)
| ```some_list[i:j]```    | Return new list - slice from element by index ```i``` till ```j-1```
| ```some_list[i:j:z]```  | Return new list - slice with step ```z```
| ```del some_list[3]```     | Remove element of index ```3``` from list ```some_list```
| ```del some_list[2:4]```   | Remove part (starting from index ```2``` till ```3```) from list ```some_list```
| ```2 in some_list```    | Return True/False - is object ```2```is part of list ```some_list```?
| ```some_list + ["a", "b"]``` | Return new list - a sum of merged lists
| ```count(x)```    | Return number of object ```x``` found in a list
| ```index(x)```    | Return first index of object ```x``` in list or raise ```ValueError``` exception if not found

Last two we saw in strings as well.


## Examples

Lists are indexable, starting at 0


```python
>>> print(some_list)
[4, 8, 15, 16, 23, 42]

>>> some_list[0]
4

>>> some_list[1]  
8

>>> some_list[2]  
15

>>> some_list[-1]
42

>>> len(some_list)
6
```

Reversing:

```python
>>> some_list.reverse()
>>> print (some_list)
[42, 23, 16, 15, 8, 4]
```
    
Merging two lists:

```python
>>> new_list = some_list + ["a", "b", "c"]
>>> print (new_list)
[4, 8, 15, 16, 23, 42, 'a', 'b', 'c']
```
    

### Sorting

> Sorting of the list with elements of different types in Python 3 forbidden.

```python
>>> some_list.sort()
>>> print(some_list)
[4, 8, 15, 16, 23, 42]
```

```python
>>> print(new_list)
[4, 8, 15, 16, 23, 42, 'a', 'b', 'c']

>>> new_list.sort()
```

Output with traceback (error):

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-57-09230de36034> in <module>()
          1 new_list
    ----> 2 new_list.sort()
    

    TypeError: unorderable types: str() < int()


But you can workaround this by using builtin function ```sorted()``` and specifying your own sorting function `key` which should return some values os the same type which later will be used for Python's regular sorting.


```python
>>> print(sorted(new_list, key=lam  bda x: str(x))) # Here we are sorting in fact by string representations
[15, 16, 23, 4, 42, 8, 'a', 'b', 'c']
```
  

### Appending, extending

> Appending - adding new element to list (one element only!)

```python
>>> some_list.append(1000)
>>> some_list
[4, 8, 15, 16, 23, 42, 1000]
```

> Extending - adding lot of new members in one operation

```python
>>> some_list = [4, 8, 15, 16, 23, 42, 1000]
>>> some_list.extend([1000, [10, 10, [20, 20]]])
>>> some_list
[4, 8, 15, 16, 23, 42, 1000, 1000, [10, 10, [20, 20]]]
```

By extending nested list Python will treat all nested as elements just as other types

```python
some_list.extend([ 0, [1,2], [3, 4]])
some_list
```
Output (3 last lines - new data):

    [4,
     8,
     15,
     16,
     23,
     42,
     1000,
     1000,
     [10, 10, [20, 20]],
     0,
     [1, 2],
     [3, 4]]



### Removing

> `pop()` removes last element from list (by default) and returns it
> Additionally it is possible to pass index of element which needs to be removed

```python
>>> some_list.pop()
[3, 4]

some_list.pop(0)
4
```

If the value being removed is not needed - removal can be done easier by `del` operator:

```python
>>> del some_list[0]
>>> del some_list[3:6]
>>> some_list
[15, 16, 23, [10, 10, [20, 20]], 0, [1, 2]]
```


### Other examples
We saw very similar examples for strings - because strings are sequence too. That is the core idea (called ducktyping) in Python - the same behavior even if the types are different.


```python
>>> some_list * 2
```
Output:

     [15,
     16,
     23,
     [10, 10, [20, 20]],
     [15, 16, 23, [10, 10, [20, 20]], 0, [1, 2]],
     0,
     [1, 2],
     15,
     16,
     23,
     [10, 10, [20, 20]],
     [15, 16, 23, [10, 10, [20, 20]], 0, [1, 2]],
     0,
     [1, 2]]


```IndexError``` exception is raised for non-existent index element


```python
some_list[1000]
```
Output:

    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-72-723edda86851> in <module>()
    ----> 1 some_list[1000]
    

    IndexError: list index out of range


### Slices

> Slices are working in the same way as in strings. They also return new lists.

```python
>>> print (some_list)
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]

>>> some_list[2:4]
[23, [10, 10, [20, 20]]]
```
    

Get new reversed list:
```python
some_list[::-1]
```
Output:



    [[1, 2],
     0,
     [15, 16, 23, [10, 10, [20, 20]], 0, [1, 2]],
     [10, 10, [20, 20]],
     23,
     16,
     15]

It is possible to assign new list to slice and change original list:

```python
>>> new_list = [1, 2, 3, 4, 5, 6]
>>> new_list[2:4] = ["a", "b", "c"]
>>> new_list
[1, 2, 'a', 'b', 'c', 5, 6]
```

Length of assigned list can differ from size of slice:

```python
>>> new_list[:1] = [100, 100, 100]
>>> new_list
[100, 100, 100, 2, 'a', 'b', 'c', 5, 6]
```

## List comprehensions
> Fast, simple and "Pythonic" way to create a list

Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition


```python
>>> cool_list = [x*2 for x in range(10)]
>>> cool_list
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

It's absolutely the same as:


```python
cool_list = []
for x in range(10):
    cool_list.append(x*2)
cool_list
```
Output:

    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

More examples:

```python
>>> [x**2 + 2*x + 1 for x in range(10)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

>>> from random import randrange
>>> [x + randrange(0, x) for x in range(1, 10)]
[1, 2, 5, 7, 6, 7, 12, 8, 14]

>>> [x + y for x in [1, 2, 3] for y in range(20, 25)]
[21, 22, 23, 24, 25, 22, 23, 24, 25, 26, 23, 24, 25, 26, 27]
```

It's possible to create nested list and use conditions as well:


```python
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

is equivalent to:

```python
combs = []
for x in [1,2,3]:
    for y in [3,1,4]:
        if x != y:
            combs.append((x, y))
```


## Deep/shallow copy

Variables in Python (name bindings) are just points to an object in memory. By assigning one variable to another we make them point to the same object which may lead to various problems.

Operator ```is``` allows comparing by ids - shows is two variables pointing to the same object 


```python
a = [1, 2, 3]
b = a
print (a is b)
a[0] = "Surprise"
print ("b is", b)
```

Output:

    True
    b is ['Surprise', 2, 3]
    

### Shallow copy of lists

Create completely new copy of the list - by creating a new list and adding elements one by one from old one

Pythonic way:

```python
b = list(a)
print (b is a)
a[0] = "Oh!"
print ("a is:", a)
print ("b is:", b)
```
Output:

    False
    a is: ['Oh!', 2, 3]
    b is: ['Surprise', 2, 3]
    
Hackish way (working but not as readable):

```python
b = a[:]
a[0] = "New"
print ("b is:", b)
print(a)
```
Output:

    b is: ['Oh!', 2, 3]
    ['New', 2, 3]
    

### Shallow copy problems
If list has mutable object deeper than on the very first nesting level - shallow copy will cause similar problems as before.


```python
a = [[1, 2], 3]
b = list(a)
a[0][0] = "Surprise!"
print (a is b)
print ("b is:", b)
```
Output:

    False
    b is: [['Surprise!', 2], 3]
    

### Deep copy

There is a special standard module for copying - ```copy```


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
Output:

    b is: [['Surprise!', 2], 3]
    c is: [[1, 2], 3]
    

### Self-referencing list

List is seqence-like object that contains pointers to other objects which are treated as it's elements.
That's why it's possible to add list to itself as element!


```python
a = [1, 2, 3]
a.append(a)
a
```
Output:

    [1, 2, 3, [...]]


In this case when we delete it - Python garbage collector won't delete from memory - because the number of reference to this object is not null

Usual Python console:
    
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

## Lists for heavy calculations

If you use list for complex math calculations - consider using numpy.


```python
import numpy
array = numpy.array(list(range(1000)))
list_ = list((range(1000)))

%timeit 999 in array
%timeit 999 in list_
```

    The slowest run took 65.02 times longer than the fastest. This could mean that an intermediate result is being cached.
    100000 loops, best of 3: 7.01 µs per loop
    100000 loops, best of 3: 18.6 µs per loop
    

## Complexity of operations

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

