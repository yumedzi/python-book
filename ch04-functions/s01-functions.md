# Functions

> Function is a series of statements which returns some value to a caller. It can also be passed zero or more arguments which may be used in the execution of the body.

> It is callable object created by using either operator `def` or `lambda`. Function is object as anything else in Python so you can assign them to variables, append to lists etc.

> Methods are functions defined inside some class.

> Functions are evaluated only when they are called.

Definition: 

🪄 _<mark style="color:green;">Code:</mark>_

```python
def function_name(arg1, arg2, ... argN): 
    <statements> 
    [return <value>]
```

Call function (execute and get it's result): 
🪄 _<mark style="color:green;">Code:</mark>_

```python
function_name(arg1, arg2, ... argN)
```

### Argument vs Parameter

> **Parameter** is the function local variable it was declared with.
> 
> **Arguments** is the variable that was passed to the function during it's call.

An example:

```py
def example(x):  #      x <-- parameter
    return str(x)
    
example(100500)  # 100500 <-- argument
```

Here:
* `x` is the *parameter*
* `100500` is the *argument*

Note: Python's official documentation often refers to *parameter* as *argument*, so *argument* can be used in most cases as more general term.

Function always returns something. You can scpecify return value by operator ```return```. If not - ```None``` will be returned. 

Python code statement can't be empty. You can "do nothing" with operator ```pass```:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def empty():
    pass
```

or even in this way (Python 3 only):


🪄 _<mark style="color:green;">Code:</mark>_

```python
def empty():
    ...
```

The function definition does not execute the function body.

The body will be executed *only* when the function is called:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def f1():
    return 1/0
print( "No complains at this point!\n" + "-"*30 )

print("Now you'll get the error:")
f1()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
No complains at this point!
------------------------------
Now you'll get the error:
```
{% endcode %}




    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-1-41e0b6328c85> in <module>()
          4 
          5 print("Now you'll get the error:")
    ----> 6 f1()
          7 


    <ipython-input-1-41e0b6328c85> in f1()
          1 def f1():
    ----> 2     return 1/0
          3 print( "No complains at this point!\n" + "-"*30 )
          4 
          5 print("Now you'll get the error:")


    ZeroDivisionError: division by zero


Function definition's execution binds the function name in the current local namespace to a function object (a wrapper around the executable code for the function). This function object contains a reference to the current global namespace as the global namespace to be used when the function is called.

In simple words, if the function accesses an object which is not defined in it - it will look in current global area:


🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 10

def foo():
    return a

print(foo()) # Will return 10 because during call global a equals to 10
a = 100500
print(foo()) # Will return 100500 because during call global a equals to 100500
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
10
100500
```
{% endcode %}



But most often the function relies on the data passed to it:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def sum(x, y=4): 
    return x * 10 + y
 
print(sum(4, 34,)) 
print(sum(y=34, x=4,))
print(sum(5))
print(sum(x=5))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
74
74
54
54
```
{% endcode %}



We can assign default argument:


🪄 _<mark style="color:green;">Code:</mark>_

```python
from random import choice

def random_phrase(length=2):
    words = ["umm", "ehmm", "I think", "unicorns", "nice", "evil"]
    
    result = []
    for _ in range(length):
        result.append(choice(words))  
    return " ".join(result)

    
print(random_phrase())
print(random_phrase(4))
print(random_phrase(length=6))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
evil unicorns
I think ehmm evil unicorns
ehmm umm unicorns evil nice unicorns
```
{% endcode %}



Using list comprehesion we can make this function very short


🪄 _<mark style="color:green;">Code:</mark>_

```python
def random_phrase(length=3):
    words = ["umm", "ehmm", "I think", "unicorns", "nice", "evil"]

    return " ".join([choice(words) for _ in ranbge(length)])

print(random_phrase(length=5))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
evil umm ehmm I think evil
```
{% endcode %}



## Arguments definitions

> Note that arguments are passed using *call by value* (where the *value* is always an *object reference*, not the value of the object


It is possible to define a function by using the following types of formal arguments: 

* Positional/Required arguments
* Keyword arguments
* Default arguments (can be positional or keyword)
* Variable-length arguments (also called arbitrary argument lists)


Schematics of these arguments and special parameters:

> `/` works from Python 3.8

🪄 _<mark style="color:green;">Code:</mark>_

```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                └ Keyword only
        └ Positional only
```

If `/` and `*` are not present in the function definition, arguments may be passed to a function by position or by keyword. We already saw these three types (positional, keyword and default).

```python 
    def sum(x, y=42):
        return x + y
```

* An example of calling function using positional arguments `x` and `y`:
    * `sum(10, 20)`

* An example of usage default argument `y`:
    * `sum(10)`
    
* An example of passing argument as keywords:
    * `sum(x=10, y=6)`
    * `sum(y=6, x=10)`

### Required arguments

> Required arguments are the arguments passed to a function in correct positional order (that's why they also known as *positional*). The number of arguments in the function call should match exactly with the function definition.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def print_strings(str1, str2): 
    print(str1, str2)
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
print_strings("Hello", "World")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Hello World
```
{% endcode %}



### Keyword arguments

> Passing arguments as key=value pair in accordance with function definition. No changes needed for function. Order of arguments when calling a function doesn't matter.

For previous example:


🪄 _<mark style="color:green;">Code:</mark>_

```python
print_strings(str1="Hello", str2="World")
print_strings(str2="James Bond", str1="Bond,")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Hello World
Bond, James Bond
```
{% endcode %}



### Default arguments

> A default argument is an argument that assumes a default value if a value is not provided in the function call for that argument.



🪄 _<mark style="color:green;">Code:</mark>_

```python
def add_friend(name, age=20): 
    print("Friend %s (%d) added" % (name, age))
    
add_friend("Mark")
add_friend(name="Mark")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Friend Mark (20) added
Friend Mark (20) added
```
{% endcode %}



### Variable-length arguments 

> You may need to process a function for more arguments than you specified while defining the function. These arguments are called variable-length arguments and are not named in the function definition, unlike required and default arguments. 

* An asterisk (```*```) is placed before the variable name that holds the values of all non-keyword variable arguments. 
* Two asterisks (```**```) are placed before the variable name that holds dictionary with keyword-variable arguments.


🪄 _<mark style="color:green;">Code:</mark>_

```python
friend1 = ("John", 25) 
add_friend(*friend1)

friend2 = dict(name="Sara", age=18) 
add_friend(**friend2)
```

    Friend John (25) added
    Friend Sara (18) added


### Order

Order of arguments of different types matters:
* Positionals:
    * required/positional
    * default positional
    * variable-length non-keyword
* Keywords:
    * keyword
    * default keyword
    * variable-length keyword

This allows avoid difficulties with understanding which argument goes to which variable.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def func(a, b, c=2): 
    return a + b + c

print( func(1, 2))
print( func(1, 2, 3)) 
print( func(c=4, a=2, b=3)) 
print( func(a=1, b=10))
print( func(10, 20, c=6))  # Correct order
#print( func(c=6, 10, 20))  # Incorrect order
```

    5
    6
    9
    13
    36



🪄 _<mark style="color:green;">Code:</mark>_

```python
print( func(3, c=6))  # Missing required arg b - exception!
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-3-e4ed5e80880e> in <module>()
    ----> 1 print( func(3, c=6))  # Missing required arg b - exception!
    

    TypeError: func() missing 1 required positional argument: 'b'


## Positional-Only parameters

> From Python 3.8 there is special syntax to mark some arguments as *positional-only*. Such arguments are placed before a `/` symbol, the rest of the parameters are not positional-only (they can be positional-or-keyword or keyword-only).

The thing is - that many built-in functions implemented in C already accept only positional arguments:


🪄 _<mark style="color:green;">Code:</mark>_

```python
help(divmod)
```

    Help on built-in function divmod in module builtins:
    
    divmod(x, y, /)
        Return the tuple (x//y, x%y).  Invariant: div*y + mod == x.
    


This is useful in many case, for example `int` has this help:

```txt
class int(object)
 |  int([x]) -> integer
 |  int(x, base=10) -> integer
...
```

But calling `int(x=100)` is ugly and incorrect while `int("100")` looks natural.

So now (from 3.8) Python has the same syntax option as in C allowing to prohibit keyword arguments:

🪄 _<mark style="color:green;">Code:</mark>_

```python
def pos_only(arg, /):
    ...
    
pos_only(42)      # OK
pos_only(arg=42)  # Error
```

## Keyword-only parameters

> There is a special syntax to mark some arguments as *keyword-only*. Those parameters go after `*` symbol in the arguments list.

Parameters marked as *keyword-only* can be passed only by keyword.

🪄 _<mark style="color:green;">Code:</mark>_

```python
def kw_only(arg, *, kwarg1, kwarg2):
    "kwarg1 and kwarg2 are keyword-only arguments"
    ...

# OK
kw_only(10, kwarg1=20, kwarg2=30)
kw_only(arg=10, kwarg1=20, kwarg2=30)

# ERROR:
kw_only(10, 20, 30)
```

Consider this function:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def files_search(files, depth=None, case_sensitive=True, include_archives=None, count_duplicates=False):
    pass
```

There is a lot of ways to call this function, and not all calls are understandable in terms of which value was passed to each argument:


🪄 _<mark style="color:green;">Code:</mark>_

```python
files_search(["1.txt", "some.log"])
files_search(["1.txt", "some.log"], 1)
files_search(["1.txt", "some.log"], 1, True)
files_search(["1.txt", "some.log"], 3, 0, True, 1)
files_search(["1.txt", "some.log"], include_archives=True)
files_search(["1.txt", "some.log"], depth=1, include_archives=True)
```

The *keyword-only* parameters definition can be used to avoid the issue what it is not possible to understand what argument was set:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def files_search(files, *, depth=0, include_archives=None, count_duplicates=True):
    pass

# OK:
files_search(["1.txt", "some.log"], depth=3, include_archives=True)
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
# ERROR:
files_search(["1.txt", "some.log"], 1, 1, True, False)
```


    

    TypeErrorTraceback (most recent call last)

    <ipython-input-7-53f9c885bca9> in <module>
          1 # ERROR:
    ----> 2 files_search(["1.txt", "some.log"], 1, 1, True, False)
    

    TypeError: files_search() takes 1 positional argument but 5 were given


## Annotations

> Mostly decorative optional feature. Used to generate more understandable help and documentation, add support for this in IDE.

🪄 _<mark style="color:green;">Code:</mark>_

```python
def foo(a: expression, b: expression = 5):
    ...
```

More examples:
🪄 _<mark style="color:green;">Code:</mark>_

```python
def compile(source: "something compilable",
            filename: "where the compilable thing comes from",
            mode: "is this a single statement or a suite?",
            program_name: str,
            make_exe: bool,
            depth: int) -> bool:
    pass
```

Usecases:
* Providing typing information
* Type checking
* Let IDEs show what types a function expects and returns
* Foreign-language bridges
* Database query mapping
* Other information
* Documentation for parameters and return values