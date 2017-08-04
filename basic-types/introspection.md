# Introspection {#Introspection}

Introspection - i.e. debugging or examining of object is very important for learning process and for production as well.

Example investigation of `str` object:

```python
>>> a = "some string"
>>> type(a)
<class 'str'>
>>> dir(a))
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', 
'__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', 
'__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', 
'__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 
'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 
'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 
'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 
'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

We see a lot of methods available in object which gives us a hint what is the kind of object it is and what we can do with it. We see here lot of methods\(functions\). Many of them are enclosed with `__` - these are called magic methods and used by Python in various situation automatically - for example if object is to be compared with another one - method `__eq__()` will be used. Other methods - like `replace` - is regular ones. If the object has attributes \(assigned variable belonging to object\) - they would be listed in dir\(\) output as well. There is no way how to distinguish between method and attribute because for Python anything is an object and method is the same as attribute with one exception - it can be called \(has magic method `__call__`\).


## Main introspection methods

Here the list of all main methods to dig into any Python object:
* `type()`
* `isinstance()`
* `id()`
* `str()`, `repr()`
* `dir()`
* `hasattr()`
* `sys.getrefcount()`, `sys.getsizeof()`



### `type()`
> returns a type of object
  
```python
>>> type("foo")
<class 'str'>
```
  
### `isinstance(x, typeA)`
> returns `True`/`False` depends if object `x`of type `typeA`
  
```python
>>> isinstance("foo", str)
True
```
  
### `id()` 
 > returns an id of object:
 
```python
>>> id("123123")
56147112
```

### `str()`, `repr()` 
> return string and "machine" representations of object. 

> `str()` is called automatically by print()

> `repr()` is called when simply type name of object in a Python interactive shell:

```python
>>> obj = "I am string"

>>> print(obj)  # str
I am string

>>> obj         # repr
'I am string'
```
  
### `dir()`

> returns a list of valid attributes for argument \(or list of names in current local scope if no argument\)

If the method of attribute name needs to be recalled - `dir()` is the best way to do this. Other way is to use [ipython](http://jupyter.org/)'s code completion \(type `some_object.` and press `TAB`\).

Introspection of an instance of some class:

```py
class A(object):      # Creating simple class
    attr1 = 5         # with one attribute: "attr1"
some_obj = A()
print(some_obj.attr1) # Checking the value of custom attribute
print(dir(some_obj))  # This will show all inherited methods and attribute we created: "attr1"
```

Output:

```py
5
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', 
'__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', 
'__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'attr1']
```

In this case we can see many inherited methods \(from parent class called "object"\) and also attributes and methods defined by us \(in this example it is just one attribute `attr1`\)

Additionally - if no arguments passed to `dir()` it will show all local variables defined (similarly to `globals()`, `locals()` functions which show global/local scopes).

### `hasattr`
In case it is needed to check if the object has some attribute hasattr\(\) is used:
```python
>>> hasattr(some_obj, "attr1")
True

>>> hasattr(some_obj, "attr2")
False
```


## module`inspect`

> low-level API for contents of a class, source code of a method, argument list for a function, detailed traceback

```python
def foo():
    print("I am top secret string")

import inspect
print("Source:\n", inspect.getsource(foo))

```
Output:

    Source:
    def foo():
        print("I am top secret string")


## module `dis`

> decompiling Python byte-code showing code execution trace

```python
import dis
dis.dis(foo)
```
Output:
```
  2           0 LOAD_GLOBAL              0 (print)
              2 LOAD_CONST               1 ('I am top secret string')
              4 CALL_FUNCTION            1
              6 POP_TOP
              8 LOAD_CONST               0 (None)
             10 RETURN_VALUE
```

