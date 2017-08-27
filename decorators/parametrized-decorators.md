# Parameterized decorators

What if we want to pass some additional argument to decorator? We can't just add this argument after function - Python won't understand that


```python
def repeater(func, times=1): # EXAMPLE OF **WRONG** DECORATOR
    def wrapper(*args):
        print("\n".join(func(*args) for i in range(times)))
    return wrapper

@repeater(100)
def test(*args):
    return "Test!"

#test = repeater(100)(test) # What is to be run actually
test()
```

Output:

    'Test!'


Let's try to pass non-default argument


```python
try:
    @repeater(5)
    def test(*args):
        return "Test!"

    test()
except TypeError as e:
    print("Got TypeError:", e)
```

    Got TypeError: 'int' object is not callable
    

If we need to pass an arg to decorator – we need to create one more wrapping function – which will return needed decorator

`def gen_deco(param)` ---> `def deco(func)`


```python
def repeater(times=1):
    "Returning result of func several time"
    def my_deco(func):
        def wrapper(*args, **kwargs):
            print("\n".join(func(*args) for i in range(times)))
        return wrapper
    return my_deco

#my_deco = repeater(3)

#@my_deco
@repeater(4) # ---> @my_deco
def test(): #  ---> test = repeater(5)(test) --> my_deco(test)
    "Return string 'Test!'"
    return "Test!"

test()
```
Output:

    Test!
    Test!
    Test!
    Test!
    

## Class-based parametrized decorators

We can achieve same functionality using classes. We'll use `__call__` method will will act as decorator and `__init__` as function that returns internal decorator.


```python
class repeater:
    def __init__(self, times=5):
        self.times = times
    
    def __call__(self, func):
        def wrapper(*args, **kwargs):
            print("\n".join(func(*args) for _ in range(self.times)))
        return wrapper

#r = repeater(2)    

@repeater(3)  # f = repeater(4)(f)
def f(x):
    return x

f("Hello Python!")
```
Output:

    Hello Python!
    Hello Python!
    Hello Python!
