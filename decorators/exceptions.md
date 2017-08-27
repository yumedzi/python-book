# Exceptions

Errors detected during execution are called **exceptions** and are not unconditionally fatal

* It is Pythonic way to use them as much often as possible
* Sometimes you can't predict all possible values and situations
    * No heaps of if else conditions

General form:

```python
try:
    <code> 
except <ExceptionName> as <alias>:
    <code in case of error happened>
else: 
    <code if everything was OK>
finally: 
    <code in any case>
```

We are checking the code only after `try` before `except`.


```python
def divide_ten(num): 
    try: 
        print(10.0 / num )
    except ZeroDivisionError: 
        print("Oops, invalid - you can't pass 0.") 
    except TypeError:
        print("Wrong type!", type(num))
    except Exception as e:
        print("Unknown exception:", e)
    else: 
        print("Cool, no exception were triggered!") 
    finally: 
        print("We're done with that.")

divide_ten("2")
print()
divide_ten(0)
print()
divide_ten(3)
```

Output:

    Wrong type! <class 'str'>
    We're done with that.
    
    Oops, invalid - you can't pass 0.
    We're done with that.
    
    3.3333333333333335
    Cool, no exception were triggered!
    We're done with that.
    

## Custom Exceptions 

```python
class CustomException(Exception): 
    def __init__(self, value): 
        self.parameter = value 
        
    def __str__(self): 
        return self.parameter
```

For raising custom Exception – `raise` used:

* `raise CustomException`

* `raise CustomException()`


```python
class NegativeException(BaseException): 
    def __init__(self, message="Can't work with negative numbers"):
        #logger.error("...")
        self.message = message
    
    def __str__(self):
        return self.message

def divide_ten(num):
    try:
        if num < 0:
            raise NegativeException
        print(10.0 / num)
    except ZeroDivisionError:
        print("Oops, can't div by zero!")
    except NegativeException as e:
        print(e.message)

divide_ten(-4)
```
Output:

    Can't work with negative numbers
    

## Referring to exceptions

Please note that `raise` can also be used to print an error message and then re-raise the exception (allowing a caller to handle the exception as well):


```python
import sys

try:
    f = open('/tmp/1.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```
Output:

    OS error: [Errno 2] No such file or directory: '/tmp/1.txt'
    

## Catching multiple exceptions

* Several except blocks
* Putting several exceptions in a tuple


```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except (IOError, ValueError) as e: 
    print("Data or file error: %s" % e )
```
Output:

    Data or file error: [Errno 2] No such file or directory: 'myfile.txt'
    

## assert

> Testing for poor ones

Debug version of raise with condition:

`assert <test>[, <data>]`

is equivalent to:

```python
if __debug__: 
    if not <test>: 
        raise AssertionError(<data>)
```

`__debug__` is special bool variable (interpreter-level constant (one of very few ones!)) which allways is True unless `python` is called with `-0` (optimization, capital O – not a zero!)

```sh
python –O script.py
```

Examples of `assert`:


```python
assert 1 == 1
assert len(range(5)) == 5
try:
    assert 2 + 2 == "2 + 2", "On paper it works..."
except AssertionError as e:
    print("Cought AssertionError:", e)
```
Output:

    Cought AssertionError: On paper it works...
    

# Context managers

> Context managers are a way of allocating and releasing some sort of resource exactly where you need it. 

```python
with open("/tmp/foo", "r") as foo: 
    print("File contents:\n", foo.read())
```

is equivalent to:

```python
foo = open("/tmp/foo", "r") 
try: 
    print("File contents:\n", foo.read())
finally: 
    foo.close()
```


### Examples of context managers

```python
import threading 
lock = threading.Lock() 

with lock: 
    my_list.append(item)
```

which is equivalent to:

```python
lock.acquire()
try: 
    my_list.append(item) 
finally:        
    lock.release()
```
