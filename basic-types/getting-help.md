## Getting help {#Getting-help}

There is a number of ways how to get help in Python - to recall how method or function works, method or attribute exact name and to dig into any object to understand it's properties better.

First of all - usual help information can be found in web and in Python itself via builtin `help`function. Just pass any function or module as argument to this function and it's documentation will be printed out. This documentation is stored in special attribute `__doc__` of the function or module.

* Help
  * In Python interactive shell:
    ```py
    help(math.sqrt)
    ```
  * Web:
    [https://docs.python.org/3/](https://docs.python.org/3/)

```py
>>> import time
>>> help(time.clock)

clock(...)
    clock() -> floating point number

    Return the CPU time or real time since the start of the process or since
    the first call to clock().  This has as much precision as the system
    records.
```

##  {#Introspection}

##  {#Introspection}


