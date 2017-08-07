# Method Resolution Order

For old class it was vertical-then-horizontal order of looking up for object attributes/methods.

> For Python 3.x and for New style classes (Python 2.5+) MRO is horizontal-then-vertical order.

## Old style class MRO

> Just for information!

```python
class A: 
    x = 'from A'

class B(A): 
    pass

class C(A): 
    x = 'from C'

class D(B, C): 
    pass

print(D.x)
```
Output:

    from A


So as you can see value of C.x is ignored even if it is "closer". This was completely redesigned.

## New style class MRO

The problem with old style classes is that if we going to inherit from base `object` we wouldn't be able to change anything. All because the logic of searching was too simple and wasn't designed for the case where everything is inherited from `object`.


```python
class A: 
    x = 'from A'

class B(A):
    pass
    
class C(A): 
    x = 'from C'

class D(B, C):
    pass
     
print(D.x)
```
Output:

    from C
    

So, what can we say about his after seeing all this crazyness? Only: "Old style classes are bad and 'Python 2, please die already! We loved you enough, now you should go. Cheers <3'"

Python (Python 2 - from 2.2 when subclassing `object` and in Python 3) used C3-linearization in case of multiple inheritance to build an order of inheritance hierarchy in which it will search for matching method/attribute.

> See this session's sources for more details about C3

To see the result of linearization of MRO - it is useful via class attribute `__mro__`.    


```python
>>> print(D.__mro__)
(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
```    

Example of complex class:

```python
class A(object): 
    x = 1
class B(object): pass
class A1(A): pass
class B1(B):
    x = 2
class C(A1, B1): pass
class C1(): pass
class D(C, C1): pass

C.__mro__
```

Output:

    (__main__.C, __main__.A1, __main__.A, __main__.B1, __main__.B, object)

```python
class A: pass
class B(A): pass
class C(B): pass
class D(B): pass
class E(C): pass
class F(D, E, B): pass

print(F.__mro__)
```
Output:

    (<class '__main__.F'>, <class '__main__.D'>, <class '__main__.E'>, <class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
    