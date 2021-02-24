## Objects in Python


```python
a = 42
```

**a** is variable

**42** is object of type **int** (integer)

* Variable - pointer to a object
* Object - specific structure in memory

So: variable holds a value. You can change the value of a variable at any point. In this case variable will just point to another object. Old object will remain but if it won't be referenced by any variable it will be cleaned out.

#### Python Objects. Short explanation:
Everything in python is object.
This includes basic types like strings, integers, lists and also - functions, classes, modules etc. Even type itself is object of class "type".
<br>
Each object has:
* id (address in memory)
* type (type object describing what kind this object is)
* value (some data pay-load)

<br>
A lot of variables can point to same object. You don't need to declare what exact type variable should be.

* Compare objects by value: ```==```
* Compare objects by id: ```is```

#### Python Objects. In-depth details:
All Python objects are special structures in memory mostly consisting of the following attributes:
* reference counter (how many variables or other links to this object exists, when it is 0 garbage collector will purge this object)
* type (pointer to another object that has information about type of current object)
* some additional contextual data
    * for digits like int, float etc. - it's the value itself
    * for sequences - pointer to structure in memory which holds member objects
    
This is what happenes when you do ```a = 42``` - you bind name ```a``` from namespace to an object ```42```. A namespace is a mapping from names (identifiers) to objects. You can rebind that name to another object (even different type than previous) - this called rebinding. Also that name can be unbindinned by ```del a```.