# Bonus stuff

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

> The following modules deal with classes that are not considered as basic, but because of their extreme importance and often usage it would be nice to take a look at them:

* Module `collections`
* Module `array`
* Module `bytearray`
* Module `enum`


### `collections`

#### `namedtuple`

> Named tuples assign meaning to each position in a tuple and allow for more readable, self-documenting code. They can be used wherever regular tuples are used, and they add the ability to access fields by name instead of position index.

Usual approach:


🪄 <mark style="color:red;">Code</mark>:

```python
student = ("John", "Jakeson", 23, "18 B")
print(f'Student {student[1]} from group {student[3]} is {student[2]} year old')
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Student Jakeson from group 18 B is 23 year old
```
{% endcode %}
To avoid the mess of various indexes we can add some light "OOP-flavor" to this use-case via `namedtuple`:


🪄 <mark style="color:red;">Code</mark>:

```python
from collections import namedtuple

Student = namedtuple("Student", "name surname age group")

student = Student("John", "Jakeson", 23, "18 B")
print(f'Student {student.name} {student.surname} from group {student.group} is {student.age} year old')
print(student)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Student John Jakeson from group 18 B is 23 year old
Student(name='John', surname='Jakeson', age=23, group='18 B')
```
{% endcode %}
To transform into dict:


🪄 <mark style="color:red;">Code</mark>:

```python
print(student._asdict())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{'name': 'John', 'surname': 'Jakeson', 'age': 23, 'group': '18 B'}
```
{% endcode %}
#### `deque`

> `deque` stands for "Double Edged Queue"

> Returns a new deque object initialized left-to-right (using append()) with data from iterable. If iterable is not specified, the new deque is empty.

While regular list is efficiently performant only when accessing it's "right side" (via `append`, `extend`, `pop` methods) `deque` (double edged queue) is efficient from left and right ends both by adding `appendleft`, `extendleft` and `popleft` methods.



🪄 <mark style="color:red;">Code</mark>:

```python
from collections import deque

de = deque("abcde") 

print(de.pop())
print(de.popleft())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
e
a
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
de.appendleft("BEGIN")
print(de)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
deque(['BEGIN', 'b', 'c', 'd'])
```
{% endcode %}
#### `defaultdict`

> `defaultdict` is a sub-class of `dict` object:

```python
defaultdict(default_factory[, ...]) --> dict with default factory
```

> If default_factory is not None, it is called without arguments to provide a default value for the given key, this value is inserted in the dictionary for the key, and returned.


🪄 <mark style="color:red;">Code</mark>:

```python
# Groupping stuff:
encountered_animals = [("birds", "eagle"), ("mammals", "hippo"), ("mammals", "panther"), 
                       ("snakes", "python"), ("birds", "hawk"), ("snakes", "anaconda")]

from collections import defaultdict

def f(animals):
    spotted_by_group = defaultdict(list)  # here list is default_factory which will be called when key will not be found
    for type_, animal in animals:
        spotted_by_group[type_].append(animal)
        
    return spotted_by_group

print(f(encountered_animals))

%timeit f(encountered_animals)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
defaultdict(<class 'list'>, {'birds': ['eagle', 'hawk'], 'mammals': ['hippo', 'panther'], 'snakes': ['python', 'anaconda']})
2.65 µs ± 144 ns per loop (mean ± std. dev. of 7 runs, 100,000 loops each)
```
{% endcode %}
The same using `setdefault` method:


🪄 <mark style="color:red;">Code</mark>:

```python
encountered_animals = [("birds", "eagle"), ("mammals", "hippo"), ("mammals", "panther"), 
                       ("snakes", "python"), ("birds", "hawk"), ("snakes", "anaconda")]

def f(encountered_animals):
    spotted_by_group = {}
    # spotted_by_group = collection.defaultdict(list) 
    for type_, animal in encountered_animals:
        #spotted_by_group[type_].append(animal)  # defaultdict
        spotted_by_group.setdefault(type_, []).append(animal)
    return spotted_by_group
    
print(f(encountered_animals))
%timeit f(encountered_animals)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{'birds': ['eagle', 'hawk'], 'mammals': ['hippo', 'panther'], 'snakes': ['python', 'anaconda']}
2.25 µs ± 24.4 ns per loop (mean ± std. dev. of 7 runs, 100,000 loops each)
```
{% endcode %}
If we set `default_factory` to `int` we can create a counter of things:


🪄 <mark style="color:red;">Code</mark>:

```python
s = 'AnnaMadrigal'
d = defaultdict(int)   #  d = {} # if via setdefault
for k in s.lower():
    # d.setdefault(k, 0) # if via setdefault
    d[k] += 1

print(d)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
defaultdict(<class 'int'>, {'a': 4, 'n': 2, 'm': 1, 'd': 1, 'r': 1, 'i': 1, 'g': 1, 'l': 1})
```
{% endcode %}
#### `Counter`

> This class is a sub-class of `dict` and used to measure how often each member is present in a given iterable

This is very similar to previous example of `defaultdict` and `int` as `default_factory`


🪄 <mark style="color:red;">Code</mark>:

```python
from collections import Counter

print(Counter(['red', 'blue', 'red', 'green', 'blue', 'blue']))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Counter({'blue': 3, 'red': 2, 'green': 1})
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
cnt = Counter('AnnaMadrigal'.lower())
print(cnt)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Counter({'a': 4, 'n': 2, 'm': 1, 'd': 1, 'r': 1, 'i': 1, 'g': 1, 'l': 1})
```
{% endcode %}
It has many useful methods:


🪄 <mark style="color:red;">Code</mark>:

```python
print(Counter("Asdasdasdasd").items())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
dict_items([('A', 1), ('s', 4), ('d', 4), ('a', 3)])
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
# elements()
print(list(cnt.elements()))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
['a', 'a', 'a', 'a', 'n', 'n', 'm', 'd', 'r', 'i', 'g', 'l']
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
# most_common(n)
print(cnt.most_common(3))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[('a', 4), ('n', 2), ('m', 1)]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
# substract
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
print(c)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```
{% endcode %}
### `array`

> New in version 3.3

> This module defines an object type which can compactly represent an array of basic values: characters, integers, floating point numbers. 

Arrays are sequence types and behave very much like lists, except that the type of objects stored in them is constrained.
The main idea is to give similar API but much less memory footprint if we need a collection of object of the same type. `array` will consume about `sizeof(one object) * len(array)` bytes.

The type is specified at object creation time by using a type code, which is a single character. The few of defined type codes ([see more in official docs](https://docs.python.org/3/library/array.html)):

|Type code   |Python Type|Minimum size in bytes|
|------------|-----------|------------------------|
|`'i'`|`int`|2
|`'h'`|`int`|2
|`'l'`|`int`|4
|`'f'`|`float`|4
|`'d'`|`float`|8
|`'b'`|`int`|1

Syntax for creating an array:

```py
array.array(typecode[, initializer])
```

Array has the similar to `list` operations like indexing and slicing. Also, `array` has these methods that are the same as in `list`:
* `append`
* `extend` 
* `count`
* `pop`
* `remove`
* `reverse`
* `index`

Some examples:


🪄 <mark style="color:red;">Code</mark>:

```python
import array

a = array.array('f', [1.2, 2.1])
print(f'Array now is {a}, item size is {a.itemsize})')

a.append(3.141516925)
print(f'After appending array is {a}')

# Emulating bytearray type:
bytes_array = array.array('b', b"ABC")
print(bytes_array)
bytes_array.frombytes(b"123")
print(bytes_array)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Array now is array('f', [1.2000000476837158, 2.0999999046325684]), item size is 4)
After appending array is array('f', [1.2000000476837158, 2.0999999046325684, 3.141516923904419])
array('b', [65, 66, 67])
array('b', [65, 66, 67, 49, 50, 51])
```
{% endcode %}
#### `numpy`

As we can see `array` is memory-optimized version of a `list` class. It doesn't have any additional methods for "mathematical"-related operations like matrix transpose, transformation, mutation, filtering and other. In case of those kinds of operations are needed - it is recommended to use powerful and famous module [`numpy`](https://numpy.org/) that has many features like:

* a powerful N-dimensional array object
* sophisticated (broadcasting) functions
* tools for integrating C/C++ and Fortran code
* useful linear algebra, Fourier transform, and random number capabilities

To install it - either run `pip install numpy` or use [Anaconda distro](https://www.anaconda.com/distribution/).

NumPy's main object is the homogeneous multidimensional array. It is a table of elements (usually numbers), all of the same type, indexed by a tuple of non-negative integers. In NumPy dimensions are called axes.


🪄 <mark style="color:red;">Code</mark>:

```python
import numpy as np

a = np.array([2,3,4])
print(f'a is {a}, type is {a.dtype}, len is {len(a)}, shape is {a.shape}')

b = np.array([(1,2,3), (4,5,6)])
print(f'b:\n{b}, shape is {b.shape}')


print(f"Transpose T:\n{b.T}")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
a is [2 3 4], type is int64, len is 3, shape is (3,)
b:
[[1 2 3]
 [4 5 6]], shape is (2, 3)
Transpose T:
[[1 4]
 [2 5]
 [3 6]]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
print("Transforming, add 0.5:\n", b + .5)
print("Transforming, add 3*b:\n", b + 3*b)
print("Transforming, mult by 3:\n", b * 3)
print("Changing shape:\n", b.reshape(1, 6))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Transforming, add 0.5:
 [[1.5 2.5 3.5]
 [4.5 5.5 6.5]]
Transforming, add 3*b:
 [[ 4  8 12]
 [16 20 24]]
Transforming, mult by 3:
 [[ 3  6  9]
 [12 15 18]]
Changing shape:
 [[1 2 3 4 5 6]]
```
{% endcode %}
### `bytearray`

> Array of bytes type (length of item is 1B)
> 
> Joke: "Mutable string", at last :)

In Python 3 string is a sequence of Unicode characters. If we encode them we will get so-called `bytes` object suitable for sending over internet or writing it to a socket or file (but usually python hides this from programmer when dealing with files using default encoding). `bytes` is analogue of the strings used in Python 2. `bytes` object is immutable, just like regular string and has the same methods.


🪄 <mark style="color:red;">Code</mark>:

```python
str_ = "Привіт, Світе!"
bytes_ = str_.encode("utf8")

print(bytes_)

print(dir(bytes_))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
b'\xd0\x9f\xd1\x80\xd0\xb8\xd0\xb2\xd1\x96\xd1\x82, \xd0\xa1\xd0\xb2\xd1\x96\xd1\x82\xd0\xb5!'
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'center', 'count', 'decode', 'endswith', 'expandtabs', 'find', 'fromhex', 'hex', 'index', 'isalnum', 'isalpha', 'isascii', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```
{% endcode %}
`bytearray` bultin type is mutable counterpart of `bytes` type.

There is no dedicated literal syntax for bytearray objects, instead they are always created by calling the constructor:

* Creating an empty instance: `bytearray()`
* Creating a zero-filled instance with a given length: `bytearray(10)`
* From an iterable of integers: `bytearray(range(20))`
* Copying existing binary data via the buffer protocol: `bytearray(b'Hi!')`


🪄 <mark style="color:red;">Code</mark>:

```python
b = bytearray(b'Hello World')
print(b)
print(b[0], b[3:6], b[:5:-1], sep=", ")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
bytearray(b'Hello World')
72, bytearray(b'lo '), bytearray(b'dlroW')
```
{% endcode %}
Good news: due to Python's duck-typing, methods of `str`, `bytes` and `bytearray` are the same, the main difference is that they return the object of the correspondent type. Also, when iterating through `bytearray`, it will yield bytecode of the character. This can sometimes overcomplicate things.


🪄 <mark style="color:red;">Code</mark>:

```python
print(b)

print(b.lower().startswith(b'hello'))
for i in b[:5:-1]:
    print(i)
    
print()
print(b''.join([chr(x).encode('utf8') for x in reversed(b[:5:-1])]))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
bytearray(b'Hello World')
True
100
108
114
111
87

b'World'
```
{% endcode %}
### `enum`

> New in version 3.4

> An enumeration is a set of symbolic names (members) bound to unique, constant values. Within an enumeration, the members can be compared by identity, and the enumeration itself can be iterated over.

In a simplified sense, this is an iteratable set of constants.

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3
```

>Member values can be anything: int, str, etc.. If the exact value is unimportant you may use auto instances and an appropriate value will be chosen for you. Care must be taken if you mix auto with other values.


🪄 <mark style="color:red;">Code</mark>:

```python
from enum import Enum, auto

class Page(Enum):
    LOGIN = auto()
    DASHBOARD = auto()
    SEARCH = auto()

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3
    
# All enum members are hashable:
color_settings_per_page = {
    Page.LOGIN: Color.RED,
    Page.DASHBOARD: Color.GREEN,
    Page.SEARCH: Color.BLUE
}
print(color_settings_per_page)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{<Page.LOGIN: 1>: <Color.RED: 1>, <Page.DASHBOARD: 2>: <Color.GREEN: 2>, <Page.SEARCH: 3>: <Color.BLUE: 3>}
```
{% endcode %}
Enums can be iterated over:


🪄 <mark style="color:red;">Code</mark>:

```python
print("We have these color options:")
for color in Color:
    print(color)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
We have these color options:
Color.RED
Color.GREEN
Color.BLUE
```
{% endcode %}
It behaves like a new type:


🪄 <mark style="color:red;">Code</mark>:

```python
print(type(Color.RED))
print(isinstance(Color.GREEN, Color))
print(Color.RED.name)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<enum 'Color'>
True
RED
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
Animal = Enum('Animal', 'ANT BEE CAT DOG')
print(Animal)
print(list(Animal))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<enum 'Animal'>
[<Animal.ANT: 1>, <Animal.BEE: 2>, <Animal.CAT: 3>, <Animal.DOG: 4>]
```
{% endcode %}
