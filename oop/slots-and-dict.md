# Slots and `__dict__`

All instance's attributes are hold in `__dict__` attribute which is a dictionary with keys as names bound to the instance.


```python
class C:
    a = 1
    
c = C()
c.b = 2
c.__dict__
```
Output:

    {'b': 2}



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
Output:

    False
    We can't access attribute b as it is not listed in __slots__
    
`__slots__` are meaninless when the class is inherited from the one which doesn't have `__slots__`.
