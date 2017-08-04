# Functions

> Function is a series of statements which returns some value to a caller. It can also be passed zero or more arguments which may be used in the execution of the body.

> It is callable object created by using either operator `def` or `lambda`. Function is object as anything else in Python so you can assign them to variables, append to lists etc.

> Methods are functions defined inside some class

> Functions are evaluated only when they are called.

Definition: 

```python
def function_name(arg1, arg2, ... argN): 
    <statements> 
    [return <value>]
```

Call function (execute and get it's result): 
```python
function_name(arg1, arg2, ... argN)
```

Function always returns something. You can scpecify return value by operator ```return```. If not - ```None``` will be returned. 

Python code statement can't be empty. You can "do nothing" with operator ```pass```.

Function definition's execution binds the function name in the current local namespace to a function object (a wrapper around the executable code for the function). This function object contains a reference to the current global namespace as the global namespace to be used when the function is called.


```python
def foo():
    return 10
foo()
```
Output:

    10


```python
def sum(x, y): 
    return x + y
 
sum(4, 34)
```

Output:


    38



The function definition does not execute the function body; this gets executed only when the function is called. 


```python
def f1():
    return 1/0
print( "No complains at this point!\n" + "-"*30 )

print("Now you'll get the error:")
f1()
    
```
Output:

    No complains at this point!
    ------------------------------
    Now you'll get the error:



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


It is possible to assign default value to argument which will be used if it will not be passed to function:

```python
from random import choice

def random_phrase(length=3):
    words = ["umm", "ehmm", "I think", "unicorns", "nice", "evil"]
    
    result = []
    for x in range(length):
        result.append(choice(words)) 
    return " ".join(result)
    
print(random_phrase())
print(random_phrase(4))
print(random_phrase(length=6))
```
Output:

    I think I think umm
    I think I think ehmm umm
    umm I think evil evil umm evil


Using list comprehension we can make this function very short

```python
def random_phrase(length=3):
    words = ["umm", "ehmm", "I think", "unicorns", "nice", "evil"]

    return " ".join([choice(words) for x in range(length)])

print(random_phrase(length=5))
```
Output:

    evil unicorns nice umm I think

