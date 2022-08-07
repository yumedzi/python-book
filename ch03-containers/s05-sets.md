# Sets

>  Set is unordered mutable collection of unique elements

Set is just like dictionary without values. Sets do not support indexing, slicing, or other sequence-like behavior.

Common uses include membership testing, removing duplicates from a sequence, and computing mathematical operations such as intersection, union, difference, and symmetric difference.

Elements can be only hashable objects - just like keys of dictionary (all immutable objects and instances of classes).

Ways to create a set:
* ```set()```
* ```{1, 2, 3}```
* ```set([1, 2, 3, 4])```
* ```set("abcdeabcde")```


```python
some_list = [1, 2, 3, 4]
some_tuple = tuple(some_list)
set_a = set(some_list)
set_b = set(some_tuple)
print(set_a)
print(set_b)
```

<sub>Output:</sub>

    {1, 2, 3, 4}
    {1, 2, 3, 4}


Main methods


```python
[method for method in dir({1}) if not method.startswith("__")]
```




<sub>Output:</sub>

    ['add',
     'clear',
     'copy',
     'difference',
     'difference_update',
     'discard',
     'intersection',
     'intersection_update',
     'isdisjoint',
     'issubset',
     'issuperset',
     'pop',
     'remove',
     'symmetric_difference',
     'symmetric_difference_update',
     'union',
     'update']



A lot of different methods for checking various mathematical set properties

## Set methods

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```len()```         | Return int - length of the set
| ```x in set_a```    | Return True/False - is object ```x```is part of the set ```set_a```?
| ```set_a``` &#124;  ```set_b``` | Return new set - a **union** (all from both)
| ```set_a & set_b``` | Return new set - a **intersection** (common to both)
| ```set_a - set_b``` | Return new set - a **difference** (those in ```set_a``` that are not in ```set_b```)
| ```set_a < set_b``` | Return **True/False** - a **issubset** (```set_a``` is proper subset of ```set_b```)
| ```set_a > set_b``` | Return **True/False** - a **issubset** (```set_b``` is proper subset of ```set_a```)