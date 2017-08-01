## Getting help {#Getting-help}

There is a number of ways how to get help in Python - to recall how method or function works, method or attribute exact name and to dig into any object to understand it's properties better.

First of all - usual help information can be found in web and in Python itself via builtin `help`function. Just pass any function or module as argument to this function and it's documentation will be printed out. This documentation is stored in special attribute `__doc__` of the function or module.

* Help
  * In Python interactive shell:
    ```py
    help(math.sqrt)
    ```
  * [Official Documentation](https://docs.python.org/3/)
  * [Stackoverflow ](https://stackoverflow.com/questions/tagged/python+python-3.x) - big community which knows (mostly) everything
    

```py
>>> import time
>>> help(time.clock)

clock(...)
    clock() -> floating point number

    Return the CPU time or real time since the start of the process or since
    the first call to clock().  This has as much precision as the system
    records.
```

This help information is stored in special attribute `__doc__` called docstring. It is the very first unassigned string in module or function or even class. Usually these strings are multiline that's why """ or ''' used to create them. It is a very nice style to fill docstrings in a code:

```py
def function_with_pep484_type_annotations(param1: int, param2: str) -> bool:
    """Example function with PEP 484 type annotations.

    Args:
        param1: The first parameter.
        param2: The second parameter.

    Returns:
        The return value. True for success, False otherwise.

    """
```  

