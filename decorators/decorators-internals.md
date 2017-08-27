# Decorators internals

Decorated function loosing it's name and docstring. In fact we are substituting one function with completely different one that just uses the first one.


```python
print("Function name:", test.__name__)
print("Function docstring:", test.__doc__)
print(test)
```
Output:

    Function name: wrapper
    Function docstring: None
    <function repeater.<locals>.deco.<locals>.wrapper at 0x103ee80d0>
    
Let's "fix" this cosmetically:

```python
test.__name__   = "test"
test.__qualname__   = "test"

print("Function name:", test.__name__)
print(test)
```
Output:

    Function name: test
    <function test at 0x103ee80d0>
    

We can do this in decorator to fix all these issues


```python
def deco(f):
    def ugly_wrapper_name(*args, **kwargs):
        return f(*args, **kwargs)
    ugly_wrapper_name.__name__ = f.__name__
    ugly_wrapper_name.__doc__ = f.__doc__
    ugly_wrapper_name.__qualname__ = f.__qualname__
    return ugly_wrapper_name

@deco
def pretty_func(x="Mew mew mew"):
    "Print something nice"
    print(x)
    
pretty_func()
print(pretty_func.__name__)
print(pretty_func.__doc__)
print(pretty_func)
```
Output:

    Mew mew mew
    pretty_func
    Print something nice
    <function pretty_func at 0x1048afea0>
    

Alternative - suggested method - to use `functools.wraps` decorator which will automatically assign wrapper function’s `__module__`, `__name__`, `__qualname__`, `__annotations__` and `__doc__`. 


```python
from functools import wraps

def my_decorator(f):
    @wraps(f)
    def wrapper(*args, **kwds):
        print('Calling decorated function')
        return f(*args, **kwds)
    return wrapper

@my_decorator
def example():
    """Docstring"""
    print('Called example function')

example()

print(example.__name__)
print(example.__doc__)
print(example)
```
Output:

    Calling decorated function
    Called example function
    example
    Docstring
    <function example at 0x104ad2ea0>
    