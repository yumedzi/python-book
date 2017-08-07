# Old and New classes

> This difference is only viable for Python 2 - as in Python 3 there are no such distinguishing as "old/new" classes.

Before Python 2.5 the format for creating a class was:

```python
class Old:
    pass
```
This was resulted in various problems with MRO and types. So some code redesigned, for this new format introduced:

```python
class New(object):
    pass
```

Differences:

1. `classobj` type as `builtin` types
2. Correct horizontal-then-vertical `MRO` (earlier it was vertical)
3. No `__new__()` method in old class
4. Additional functionality: 
    1. `__slots__` (Python 3.x)
    2. `__getattribute__`
    3. `__getattr__` and `__getattribute__` don't look for magic methods in instance
