## Type Hints

Some other languages such as Java/C++ (but not Python) have static typing. It allows to define all variables and return values of functions declaring which type of object those will be. The predefined types allow the compilers to check the code before compiling and running the program. Additionally IDE has better options to suggest available methods and linters - to check the correct way of working with objects.

In Python we can enable this be declaring types for each defined variable, function parameter and function return value.

Using type hints will give us these benefits:
* Code will be much easier to read as it will be clear what types of object is supposed to be used.
* IDE can suggest better auto completion results.
* Linters/Type checkers like `mypy` can validate code against correctness and we can find out about problem before running without complex debugging.

Type hints are created using annotations - colon followed by a type we want to correlate with our parameter or return value.

Let's check the following function, it is quite hard to tell what types for which parameter this function expects:


```python
def calc_square_ugly(x, y, u):
    return f"{x * y} {u}²" 
```

It would much more clear if we know what types to use. In the following example we see that `x` and `y` are `int` and `u` is of `str` type, additionally we now know that the function is going to return `str`:


🪄 <mark style="color:red;">Code</mark>:

```python
def calc_square(x: int, y: int, u: str="m") -> str:
    return f"{x * y} {u}²" 

print(calc_square(5, 4))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
20 m²
```
{% endcode %}
If we complement example above with some docstring the type hints will be a bonus part of the help information about our new function:


🪄 <mark style="color:red;">Code</mark>:

```python
def calc_square(x: int, y: int, u: str="m") -> str:
    """
    Calculate square of a rectangle with sizes x and y.
    Return a string with calculated value followed by units (meters) by default.
    """
    return f"{x * y} {u}²" 

help(calc_square)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Help on function calc_square in module __main__:

calc_square(x: int, y: int, u: str = 'm') -> str
    Calculate square of a rectangle with sizes x and y.
    Return a string with calculated value followed by units (meters) by default.
```
{% endcode %}
