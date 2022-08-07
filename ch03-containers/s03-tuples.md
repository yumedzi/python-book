# Tuples

> Tuple is ordered immutable sequence of objects. They are used when memory counts, when we don't want to change members accidentally, for passing arguments etc.

> Syntactically, a tuple is a comma-separated sequence of values. It is not necessary, but it is conventional to enclose tuples in parentheses.

It is not possible to change it's elements after creation. It's like unchangeable list or string where instead of characters are any kind of objects.

Because tuple is sequence it is very similar to list and what is appliable to list and not changing it - will for sure be possible to with a tuple.

Ways to create a tuple:
* ```tuple()```
* ```()```
* ```(1,)```
* `1,`
* `tuple([1])`  `# (1,)`
* ```(1, 2, 3, [10, 20], 5)```
* `1, 2, 3`

Creating a tuple with 1 element requires comma because without it Python consider such expression as logic grouping.


```python
(1)
```




<sub>Output:</sub>

    1




```python
(1,)  
```




<sub>Output:</sub>

    (1,)



In fact parences are not needed, they are just for readability:


```python
1,
```




<sub>Output:</sub>

    (1,)




```python
1, 2, 3
```




<sub>Output:</sub>

    (1, 2, 3)



## Main methods of tuple


```python
some_tuple = 1, 2, 100, 15
print( dir(some_tuple))  # Yep, again all methods
```

<sub>Output:</sub>

    ['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'count', 'index']


That's right - if not counting magic methods - not many at all. Just ```count``` and ```index```!

### Tuple methods

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```some_tuple[i]```     | Return element by index ```i``` (int)
| ```some_tuple[i:j]```   | Return new tuple - slice from element by index ```i``` till ```j-1```
| ```some_tuple[i:j:z]```  | Return new tuple - slice with step ```z```
| ```count(x)```          | Return number of object ```x``` found in a tuple
| ```index(x)```          | Return first index of object ```x``` in tuple or raise `ValueError` if not found
| ```x in some_tuple```   | Return True/False - is object ```x```is part of list ```some_tuple```?
| ```some_tuple + ("a", "b") ``` | Return new tuple - a result of two tuples merging

## Examples


```python
some_tuple[:2]
```




<sub>Output:</sub>

    (1, 2)




```python
some_tuple + (4, "a")
```




<sub>Output:</sub>

    (1, 2, 100, 15, 4, 'a')




```python
100 in some_tuple
```




<sub>Output:</sub>

    True



## Tuple unpacking


```python
a, b = 1, 2 
print(a, b)
```

    1 2



```python
a, b = b, a
print(a, b)
```

    2 1


Available only in Python 3:


```python
a, *b, c = 1, 2, 3, 4, 5, 6, 7
print("a is {}, b is {}, c is {}".format(a, b, c))
```

    a is 1, b is [2, 3, 4, 5, 6], c is 7



```python
f = lambda: (1, 2, 232, 12, 123, 123, 123, 123)
x, *_ = f()
print(x)
```

    1


## Tuples vs Lists


The main difference is that tuple is immutable sequence while list is mutable. Some may even call tuple "immutable list" which may have some sense in practice but from architectural point of view is not very correct.

The design purpose of tuple is to store **heterogeneous** data (objects of different kinds or meaning) while list is intendent to store **homogeneous** data (objects of the same kind, type, meaning). 

> Tuples are immutable sequences, typically used to store collections of heterogeneous data (such as the 2-tuples produced by the enumerate() built-in). Tuples are also used for cases where an immutable sequence of homogeneous data is needed (such as allowing storage in a set or dict instance.

For heterogeneous collections of data where access by name is clearer than access by index, **collections.namedtuple()** may be a more appropriate choice than a simple tuple object.

In other words:
* use tuple for structure
* use list for order/sequencing

### Examples

* Parts of datetime are different kinds, so it is tuple:

```python
# python 2
>>> import time
>>> time.localtime()
(2017, 5, 17, 9, 59, 54, 2, 137, 0)
```


```python
import datetime

for i in datetime .datetime.now().timetuple():
    print(i, end=", ")
    
datetime.datetime.now()
```

    2019, 5, 24, 10, 30, 37, 4, 144, -1, 




    datetime.datetime(2019, 5, 24, 10, 30, 37, 749557)



* Values is result of range() are all of the same type, so it is list (in Python 2):

```python
# python 2
>>> range(10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```


```python
list(range(10))
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



* Coordinates:

```python
# one coordinate is a tuple, each member is different kind of value (X, Y)
point_a = (20, 13)
point_b = (13, 14)

# sequence of coordinates is list
visited_points = [(12, 10), (4, 16)]
unknown_points = [point_a, point_b]

# using tuple we could assign value to it in dict (hashmap data structure)
temperatures = {
    point_a: 25.5,
    point_b: 34.12,
    (12, 34): 28.19
}
```