# Argument passing

You can call/define a function by using the following types of formal arguments: 
* Required arguments
* Keyword arguments
* Default arguments
* Variable-length arguments


Two first three types we saw previously:

* Required arguments - also called positional

    ```sum(5, 3)```

* Default argument, ```length``` with default value ```3```:

    ```random_phrase(length=3)```

* Keyword arguments, passing ```x``` and ```y```:

    ```sum(x=10, y=6)```

### Required arguments

> Required arguments are the arguments passed to a function in correct positional order. The number of arguments in the function call should match exactly with the function definition.


```python
def print_strings(str1, str2): 
    print(str1, str2)

print_strings("Hello", "World")
```
Output:

    Hello World


### Keyword arguments

> Passing arguments as key=value pair in accordance with function definition. No changes needed for function. Order of arguments when calling a function doesn't matter.

For previous example:


```python
print_strings(str1="Hello",  str2="World")
print_strings(str2="James Bond", str1="Bond,")
```
Output:

    Hello World
    Bond, James Bond


### Default arguments

> A default argument is an argument that assumes a default value if a value is not provided in the function call for that argument.



```python
def add_friend(name, age=20): 
    print("Friend %s (%d) added" % (name, age))
    
add_friend("Mark")
add_friend(name="Mark")
```
Output:

    Friend Mark (20) added
    Friend Mark (20) added


### Variable-length arguments 

> You may need to process a function for more arguments than you specified while defining the function. These arguments are called variable-length arguments and are not named in the function definition, unlike required and default arguments. 

* An asterisk (```*```) is placed before the variable name that holds the values of all non-keyword variable arguments. 
* Two asterisks (```**```) are placed before the variable name that holds dictionary with keyword-variable arguments.


```python
friend1 = ("John", 25) 
add_friend(*friend1)

friend2 = dict(name="Sara", age=18) 
add_friend(**friend2)
```
Output:

    Friend John (25) added
    Friend Sara (18) added


### Order

Order of arguments of different types matters:
* positional
* keyword
* default
* variable-length non-keyword
* variable-length keyword

This allows avoid difficulties with understanding which argument goes to which variable.


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
Output:

    5
    6
    9
    13
    36



```python
print( func(3, c=6))  # Missing required arg b - exception!
```
Output:

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-3-e4ed5e80880e> in <module>()
    ----> 1 print( func(3, c=6))  # Missing required arg b - exception!
    

    TypeError: func() missing 1 required positional argument: 'b'


## Keyword-only arguments

> There is a special syntax to mark some arguments as keyword-only

> `def foo(arg1, arg2, *, kwarg1, kwarg2)` <-- here kwarg1 and kwarg2 can be only keyword arguments

Consider this function:


```python
def files_search(files, depth=None, include_archives=None, count_duplicates=None):
    pass
    
files_search(["1.txt", "some.log"])
files_search(["1.txt", "some.log"], 1)
files_search(["1.txt", "some.log"], 1, True)
files_search(["1.txt", "some.log"], 1, 1, 1)
files_search(["1.txt", "some.log"], include_archives=True)
files_search(["1.txt", "some.log"], 1, include_archives=True)
```

This sometimes can lead to a mess because you can't quickly understand what argument was set.
For such cases there a special syntax to disable non-keyword arguments after som point:


```python
def files_search(files, *, depth=None, include_archives=None):
    pass
files_search(["1.txt", "some.log"], depth=3, include_archives=True)
files_search(["1.txt", "some.log"], 1, 1)
```
Output:

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-49-a8e04519ddb8> in <module>()
          2     pass
          3 files_search(["1.txt", "some.log"], depth=3, include_archives=True)
    ----> 4 files_search(["1.txt", "some.log"], 1, 1)
    

    TypeError: files_search() takes 1 positional argument but 3 were given


## Annotations

> Mostly decorative optional feature. Used to generate more understandable help and documentation, add support for this in IDE.

```python
def foo(a: expression, b: expression = 5):
    ...
```

More examples:
```python
def compile(source: "something compilable",
            filename: "where the compilable thing comes from",
            mode: "is this a single statement or a suite?"):
    ...
```

Usecases:
* Providing typing information
* Type checking
* Let IDEs show what types a function expects and returns
* Foreign-language bridges
* Database query mapping
* Other information
* Documentation for parameters and return values

