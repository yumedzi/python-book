# Lists

> List is ordered mutable sequence of ANY objects.

> This means that it is allowed to change it's elements after creation: adding new, changing/removing existing etc.

Ways to create a list:

* `[]`
* `list()`
* `[1, 2, 3, [10, 20], 5]`

### Main methods

🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list = [4, 8, 15, 16, 23, 42]
print(dir(some_list))  # Again all methods
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```
{% endcode %}

Actually beside magical methods (containing \_\_) there are not so much methods left

Worth to note that most methods are not returning anything - they are just directly changing the list itself because it is mutable object.

#### List methods

| Method(s)          | Description                                          |
| ------------------ | ---------------------------------------------------- |
| `len(some_list)`   | Return int - length of the list                      |
| `reverse()`        | Reverse order of elements of the list in place       |
| `sort()`           | Sort elements of the list in place                   |
| `append(x)`        | Add new element `x` to the end of the list           |
| `extend(iterable)` | Append elements of iterable to the end of the list   |
| `pop()`            | Return and remove the last element from the list     |
| `pop(i)`           | Return and remove element by index `i` from the list |

| Method(s)                | Description                                                          |
| ------------------------ | -------------------------------------------------------------------- |
| `some_list[i]`           | Return (or assign) element by index `i` (int)                        |
| `some_list[i:j]`         | Return new list - slice from element by index `i` till `j-1`         |
| `some_list[i:j:z]`       | Return new list - slice with step `z`                                |
| `del some_list[3]`       | Remove element of index `3` from list `some_list`                    |
| `del some_list[2:4]`     | Remove part (starting from index `2` till `3`) from list `some_list` |
| `2 in some_list`         | Return True/False - is object `2`is part of list `some_list`?        |
| `some_list + ["a", "b"]` | Return new list - a sum of merged lists                              |

| Method(s)  | Description                                                                           |
| ---------- | ------------------------------------------------------------------------------------- |
| `count(x)` | Return number of object `x` found in a list                                           |
| `index(x)` | Return first index of object `x` in list or raise `ValueError` exception if not found |

Last two we saw in strings as well.

## Examples

Lists are indexable, starting at 0

🪄 _<mark style="color:green;">Code:</mark>_

```python
print (some_list)
some_list[0]
```

📟 _<mark style="color:green;">Output:</mark>_

```
[4, 8, 15, 16, 23, 42]





4
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list[2]
```

📟 _<mark style="color:green;">Output:</mark>_

```
15
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list[-1]
```

📟 _<mark style="color:green;">Output:</mark>_

```
42
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
print (some_list)
len(some_list)
```

📟 _<mark style="color:green;">Output:</mark>_

```
[4, 8, 15, 16, 23, 42]





6
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list.reverse()
print (some_list)
```

📟 _<mark style="color:green;">Output:</mark>_

```
[42, 23, 16, 15, 8, 4]
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list.sort()
print (some_list)
```

📟 _<mark style="color:green;">Output:</mark>_

```
[4, 8, 15, 16, 23, 42]
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
new_list = some_list + ["a", "b", "c"]
print (new_list)
```

📟 _<mark style="color:green;">Output:</mark>_

```
[4, 8, 15, 16, 23, 42, 'a', 'b', 'c']
```

### Sorting

> Sorting of the list with elements of different types in Python 3 is forbidden (yields an TypeError exception about unsupported `'<'` operation).

```python
new_list 
new_list.sort()
```

```
TypeErrorTraceback (most recent call last)

<ipython-input-9-a8ad78a8eda3> in <module>()
      1 new_list
----> 2 new_list.sort()


TypeError: '<' not supported between instances of 'str' and 'int'
```

But we can workaround this by using builtin function `sorted()` and specifying your own sorting function `key` which should return some values os the same type which later will be used for Python's regular sorting.

```python
print(sorted(new_list, key=str)) # Here we are sorting in fact by string representations
```

```
[15, 16, 23, 4, 42, 8, 'a', 'b', 'c']
```

### Appending, extending

```python
some_list.append(1000)
some_list
```

```
[4, 8, 15, 16, 23, 42, 1000]
```

```python
some_list = [4, 8, 15, 16, 23, 42, 1000]
some_list.extend([1000, [10, 10, [20, 20]], some_list])
some_list
```

```
[4, 8, 15, 16, 23, 42, 1000, 1000, [10, 10, [20, 20]], [...]]
```

By extending nested list Python will treat all nested as elements just as other types

```python
some_list.extend([ 0, [1,2], [3, 4]])
some_list
```

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

### Removing

```python
some_list.pop()
```

```
[3, 4]
```

```python
some_list.pop(0)
```

```
4
```

```python
del some_list[0]
del some_list[3:6]
```

```python
some_list
```

```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]
```

### Other examples

We saw very similar examples for strings - because strings are sequence too. That is the core idea (called ducktyping) in Python - the same behavior even if the types are different.

```python
some_list * 2
```

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

```python
some_list[::-1]
```

```
[[1, 2],
 0,
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 [10, 10, [20, 20]],
 23,
 16,
 15]
```

```python
some_list[:4]
```

```
[15, 16, 23, [10, 10, [20, 20]]]
```

```python
some_list[2:]
```

```
[23,
 [10, 10, [20, 20]],
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 0,
 [1, 2]]
```

```python
print (some_list)
some_list[-2]
```

```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]





0
```

```python
(some_list * 4)[::4]
```

```
[15,
 [15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]],
 16,
 0,
 23,
 [1, 2],
 [10, 10, [20, 20]]]
```

`IndexError` exception is raised for non-existent index element

```python
some_list[1000]
```

```
IndexErrorTraceback (most recent call last)

<ipython-input-24-a1d5b08ec438> in <module>()
----> 1 some_list[1000]


IndexError: list index out of range
```

## List slices

Slices of list object are a bit different to the slices of strings due to the fact that lists are mutable. Because of these additional operations are available:

* slice deletion
* slice assignment

Firstly, let's check regular list slice obtaining:

### Slice obtaining

```python
print (some_list)
some_list[2:4]
```

```
[15, 16, 23, [10, 10, [20, 20]], [...], 0, [1, 2]]





[23, [10, 10, [20, 20]]]
```

```python
some_list[2:4] = ["a", "b", "c"]
some_list
```

```
[15, 16, 'a', 'b', 'c', [...], 0, [1, 2]]
```

```python
some_list[:1] = [100, 100, 100]
some_list
```

```
[100, 100, 100, 16, 'a', 'b', 'c', [...], 0, [1, 2]]
```

### Slice deletion

By using `del` operator on the slice it is possible to delete target part from the original list:

```python
list_ = list(range(1, 6))
print("Before:", list_)

del list_[2:4]
print("After:", list_)
```

```
Before: [1, 2, 3, 4, 5]
After: [1, 2, 5]
```

### Slice assignment

By assignining the slice to another iterable, the content of that iterable will be used to replace the target part of the original list:

```python
list_ = list(range(1, 6))
print("Before:", list_)

list_[2:4] = ["A"]
print("After:", list_)
```

```
Before: [1, 2, 3, 4, 5]
After: [1, 2, 'A', 5]
```

## List comprehensions

> Fast, simple and "Pythonic" way to create a list

Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition

```python
cool_list = [x*2 for x in range(10)]
cool_list
```

```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

It's absolutely the same as:

```python
cool_list = []
for x in range(10):
    cool_list.append(x*2)
cool_list
```

```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

```python
[x**2 + 2*x + 1 for x in range(10)]
```

```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

```python
# Random list (len till 15) from rand ints (till 10)
from random import randrange
[randrange(0, 10) for _ in range(randrange(3, 15))]
```

```
[2, 2, 4, 8, 9, 2, 4]
```

```python
[f"{x}-{y}" for x in [1, 2, 3] for y in "ABC"]
```

```
['1-A', '1-B', '1-C', '2-A', '2-B', '2-C', '3-A', '3-B', '3-C']
```

```python
list_ = []
for x in [1, 2, 3]:
    for y in "ABC":
        list_.append(f"{x}-{y}")
print(list_)
```

```
['1-A', '1-B', '1-C', '2-A', '2-B', '2-C', '3-A', '3-B', '3-C']
```

The order of loops matters:

```python
[f'{x}-{y}' for x in "abc" for y in range(1, 4)]
```

```
['a-1', 'a-2', 'a-3', 'b-1', 'b-2', 'b-3', 'c-1', 'c-2', 'c-3']
```

```python
[f'{x}-{y}' for y in range(1, 4) for x in "abc"]
```

```
['a-1', 'b-1', 'c-1', 'a-2', 'b-2', 'c-2', 'a-3', 'b-3', 'c-3']
```

It's possible to create nested list and use conditions as well:

```python
[(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
```

```
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

is equivalent to:

```python
combs = []
for x in [1, 2, 3]:
    for y in [3, 1, 4]:
        if x != y:
            combs.append((x, y))
combs
```

```
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

Some "real-world" example:

```python
[func(x, y) for x in list_x for y in list_y if check(x, y)]
```

## Deep/shallow copy

🔥

Variables in Python (name bindings) are just points to an object in memory. By assigning one variable to another we make them point to the same object which may lead to various problems.

Operator `is` allows comparing by ids - shows is two variables pointing to the same object

```python
a = [1, 2, 3]
b = a
print (a is b)
a[0] = "Surprise"
print ("b is", b)
```

```
True
b is ['Surprise', 2, 3]
```

### Shallow copy of lists

Create completely new copy of the list - by creating a new list and adding elements one by one from old one

```python
b = a.copy() # Pythonic way
b = list(a) # Almost Pythonic way
b = a[:] # hacker way

print (b is a)
a[0] = "Oh!"
print ("a is:", a)
print ("b is:", b)
```

```
False
a is: ['Oh!', 2, 3]
b is: ['Surprise', 2, 3]
```

```python
b = a[:]  # Hackish way
a[0] = "New"
print ("b is:", b)
print(a)
```

```
b is: ['Oh!', 2, 3]
['New', 2, 3]
```

### Shallow copy problems

If list has mutable object deeper than on the very first nesting level - shallow copy will cause similar problems as before.

```python
a = [[1, 2], 3]
b = list(a)
a[0][0] = "Surprise!"
print (a is b)
print ("b is:", b)
```

```
False
b is: [['Surprise!', 2], 3]
```

### Deep copy

There is a special standard module for copying - `copy`

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

```
b is: [['Surprise!', 2], 3]
c is: [[1, 2], 3]
```

### Self-referencing list

List is seqence-like object that contains pointers to other objects which are treated as it's elements. That's why it's possible to add list to itself as element!

```python
a = [1, 2, 3]
a.append(a)
print(a)
print(a[-1][-1][-1][-1][-1][-1][-1])
```

```
[1, 2, 3, [...]]
[1, 2, 3, [...]]
```

In this case when we `del`ete it - Python garbage collector won't delete from memory - because the number of reference to this object is not null

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

### Lists for heavy calculations

If you use list for complex math calculations - consider using `numpy`.

```python
import numpy
array = numpy.array(list(range(1000)))
list_ = list((range(1000)))

%timeit 999 in array
%timeit 999 in list_
```

```
12.2 µs ± 35.2 ns per loop (mean ± std. dev. of 7 runs, 100000 loops each)
29.7 µs ± 68.2 ns per loop (mean ± std. dev. of 7 runs, 10000 loops each)
```

## Complexity of operations

🔥

Time-complexity (aka "Big O" or "Big Oh") of various operations in current CPython.

> Generally, 'n' is the number of elements currently in the container. 'k' is either the value of a parameter or the number of elements in the parameter.

| Operation   | Average Case | Amortized Worst Case |
| ----------- | ------------ | -------------------- |
| Copy        | O(n)         | O(n)                 |
| Append      | O(1)         | O(1)                 |
| Insert      | O(n)         | O(n)                 |
| Get Item    | O(1)         | O(1)                 |
| Set Item    | O(1)         | O(1)                 |
| Delete Item | O(n)         | O(n)                 |

| Operation      | Average Case | Amortized Worst Case |
| -------------- | ------------ | -------------------- |
| Iteration      | O(n)         | O(n)                 |
| Get Slice      | O(k)         | O(k)                 |
| Del Slice      | O(n)         | O(n)                 |
| Set Slice      | O(k+n)       | O(k+n)               |
| Extend         | O(k)         | O(k)                 |
| Sort           | O(n log n)   | O(n log n)           |
| Multiply       | O(nk)        | O(nk)                |
| x in s         | O(n)         |                      |
| min(s), max(s) | O(n)         |                      |
| Get Length     | O(1)         | O(1)                 |

As we can see from [Complexity of operations](s02-lists.md#Complexity-of-operations) section, `list` has fast (complexity is `O(1)`) such methods as `append` and `pop` which work with right end of the structure. So this is a _FILO_ structure - "stack". So, if we want to achieve maximum performance we should use list as stack (and not use `insert(0, x)` and `pop(0)` methods).
