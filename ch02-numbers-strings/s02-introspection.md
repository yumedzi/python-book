## Introspection

* Checking id of object: `id()`
    * Check that objects have same id: `is` (opposite check: `is not`)
* Checking the type of object/variable:
    * ```type()``` - returns a type of object
    * ```isinstance(x, typeA)``` - returns True/False depends if object ```x``` of type ```typeA```

* ```dir()``` - return a list of valid attributes for argument (or list of names in current local scope if no argument)
* module `inspect` - low-level API for contents of a class, source code of a method, argument list for a function, detailed traceback
* module `dis` - decompiling Python byte-code showing code execution trace

Example of introspection of int object:


```python
a = 42
print(dir(a))
```

    ['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']


We see a lot of methods available in object which gives us a hint what is the kind of object it is and what we can do with it.

Introspection of an instance of some class:


```python
class A(object):      # Creating simple class
    attr1 = 5         # with one attribute: "attr1"
some_obj = A()
print(some_obj.attr1) # Checking the value of custom attribute
print(dir(some_obj))  # This will show all inherited methods and attribute we created: "attr1"
```

    5
    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'attr1']


In this case we can see many inherited methods (from parent class called "object") and also attributes and methods defined by us (in this example it is just one attribute "attr1")