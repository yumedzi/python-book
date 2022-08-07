# Magic attributes and methods

## Builtin class attributes:

* `__name__`
* `__doc__`
* `__module__`   
* `__dict__`
* `__class__`


🪄 _<mark style="color:green;">Code:</mark>_

```python
class A:
    "Our great class" 
    x = 1
```

## Magic methods 

> `__<method>__`

* `__init__`
    * Initializing instance   
* `__new__`
    * Instance constructor
* `__repr__`
    *  Representation of an object  
* `__str__`
    *  String representation   
* `__del__`
    *  Deletion of object(called when del used and count to obj is 0)

### Instance constructor

`__new__()`

* First method for creating new object
* It is **static method**
* Invoked before `__init__()`, need to return object
* Works with ```cls``` (class object, as instance is not created yet)
* Old style class don't have this method!

🪄 _<mark style="color:green;">Code:</mark>_

```python
def __new__(cls):
    return super().__new__(cls)
```

### Instance initializer

`__init__()`

* It is not a constructor (there is `__new__()` for that)
* `__init__()` takes an already created object and fills required attributes according to declared logic first arg is `self`
* Doesn't return anything (it returns `None`), just assigning attributes to an object.

🪄 _<mark style="color:green;">Code:</mark>_

```python
def __init__(self, name): 
    self.name = name
```

### Representations

`__str__(self)` 

* String representation – for **humans**
* Used when `str(obj)` or `print(obj)`

`__repr__(self)`

* Representation for **"machines"**
* Ideal case: `eval(repr(obj)) --> obj`
* Used when calling `repr(obj)` or just `obj` in Python session



🪄 _<mark style="color:green;">Code:</mark>_

```python
print(A())
A()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
<__main__.A object at 0x7ff51775b4a8>
{% endcode %}






    <__main__.A at 0x7ff51775b4e0>



### Hash

`__hash__(self)`

* Called by hashed collections:
    * `set`
    * `frozenset`
    * `dict`
* In simplest case as for instances it is based on `id(self)` so all objects are different


🪄 _<mark style="color:green;">Code:</mark>_

```python
A().__hash__()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
8793164831643
{% endcode %}




### Bases 

`__bases__` (attribute)

* Tuple (possibly empty or a singleton) containing the base classes, in the order of their occurrence in the base class list 


```python
class A: pass

A.__bases__
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
(object,)
{% endcode %}




### Docstring

`__doc__` (attribute)

* Class’s documentation string, or None if undefined.


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(A.__doc__)
help(A)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
None
Help on class A in module __main__:
{% endcode %}

    
    class A(builtins.object)
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    


### Module

`__module__`  (attribute)

* Module name in which the class is defined. This attribute is `"__main__"` in interactive mode.


🪄 _<mark style="color:green;">Code:</mark>_

```python
A.__module__
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
'__main__'
{% endcode %}




### Boolean value

`__bool__(self)` (`__nonzero__` for Python 2)

* Used when `bool(obj)`
* By default - True


🪄 _<mark style="color:green;">Code:</mark>_

```python
bool(A())
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
True
{% endcode %}




### Comparison

`__eq__(self, other)`

* Return `True` if objects are equal

`__gt__(self, other)`

* Return `True` if `self > other`

Other methods:
* `__ne__(self, other)   # !=`
* `__ge__(self, other)   # >=`
* `__lt__(self, other)   # <`
* `__le__(self, other)   # <=`


It is really a pain to fill all of those!

Battery: `functools.total_ordering`


```python
import functools

@functools.total_ordering
class Something:
    value = 1
    
    def __eq__(self, other):
        return self.value == other.value
    
    def __gt__(self, other):
        return self.value > other.value
    
b1 = Something()
b1.value = 5
b2 = Something()
print(b1 >= b2)
print(b1 <= b2)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
True
False
{% endcode %}



### Iterator protocol

`__iter__(self)`

* Returns iterator for given object (or `self` if it is iterator)

`__next__(self)` (`next(self)` for Python 2.x)

* Return next value for iterator-like object

### Call

Object can be `callable` (function-like object).

`__call__(self, *args)`

This is very useful to call the method which used very often.



# Slots and `__dict__`

All instance's attributes are hold in `__dict__` attribute which is a dictionary with keys as names bound to the instance.


```python
class C:
    a = 1


c = C()
c.b = 2
c.__dict__
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
{'b': 2}
{% endcode %}




> `__slots__` is a list with instance attributes that can be assigned

This is needed to suppress automatic creation of `__dict__` - this can be useful when we have a lot of simple objects and their dictionaries are taking too much space. Also slots are limiting attributes that can be assigned to an object.


```python
class D:
    __slots__ = ("a", )


d = D()
print(hasattr(d, "__dict__"))
d.a = 5  # OK
try:
    d.b = 5
except AttributeError:
    print("We can't access attribute b as it is not listed in __slots__")
```

    False
    We can't access attribute b as it is not listed in __slots__


`__slots__` are meaninless when the class is inherited from the one which doesn't have `__slots__`.