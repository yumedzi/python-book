# Doctest

> The simplest, easiest and funniest way to "home-test" code

The name is short for "document testing" or "testable document".

Doctest are great for non-production usage, small projects, tasks and for documentation purposes

Ideally, `doctest` informs human readers, and tells the computer what to expect at the same time

* Mixing tests and documentation helps us:
* Keeps the documentation up-to-date with reality
* Make sure that the tests express the intended behavior
* Reuse some of the efforts involved in the documentation and test creation

## Syntax

* Lines that start with a `>>>` prompt are sent to a Python interpreter.

* Lines that start with a `...` prompt are sent as continuations of the code from the previous line, allowing you to embed complex block statements into your doctests.

* Finally, any lines that don't start with `>>>` or `...`, up to the next blank line or `>>>` prompt, represent the output expected from the statement.


🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def some_func(x, y=0):
    '''
    My little function to summarize a few numbers:
    >>> some_func(5, 1)
    6
    
    Also, second arg is optional
    >>> some_func(5)
    5
    '''
    return x + y

if __name__ == '__main__':
    import doctest
    doctest.testmod(verbose=True)
```


```
Trying:
    some_func(5, 1)
Expecting:
    6
ok
Trying:
    some_func(5)
Expecting:
    5
ok
1 items had no tests:
    __main__
1 items passed all tests:
   2 tests in __main__.some_func
2 tests in 2 items.
2 passed and 0 failed.
Test passed.
```

We can test anything that can be typed in interactive Python shell:

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def some_func():
    '''
    We can even create a new function here:
    >>> def sum(x, y):
    ...   return x + y
    >>> sum(3, 6)
    9
    '''
```


Doctests can be keeped in plain txt files

The doctest module ignores anything in the file that isn't part of a test

```shell
python –m doctest test.txt -v
```

Doctests can be keeped in docstrings in:
* modules
* functions
* classes
* class methods


The simplest way to start using doctest:
```python
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

Simplest testing ever!

**test_example.py**
🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def sum_nums(*args):
    """
    >>> sum_nums(1, 2)
    3
    >>> sum_nums()
    0
    >>> sum_nums('a', 'b')
    Traceback (most recent call last):
    ...
    TypeError: sum() can't sum strings [use ''.join(seq) instead]
    """
    return sum(args)

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```


```shell
$ python test_example.py –v
Trying:
sum_nums(1, 2)
Expecting:
3
ok
Trying:
sum_nums()
Expecting:
0
ok
Trying:
sum_nums('a', 'b')
Expecting:
Traceback (most recent call last):
...
TypeError: unsupported operand type(s) for +: 'int' and 'str'
ok
...
```

## Expecting exceptions

Exception tracebacks tend to contain many details that are not relevant to the test, but that can change unexpectedly.
* The doctest module deals with this by ignoring the traceback entirely: it's only concerned with the first line:

```python
Traceback (most recent call last):
<Exception>: <expected details>
```

* which tells it that you expect an exception, and the part after the traceback, which tells it which exception you expect.
* The doctest module only reports a failure if one of these parts does not match.

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> 1/0
Traceback (most recent call last):
ZeroDivisionError: integer division or modulo by zero

>>> def epic_fail():
... return [x for x in [1, 2, 3, 4, 5)
Traceback (most recent call last):
SyntaxError: invalid syntax
```


## Expecting blank lines

The doctest handles this situation by matching a line that contains only the text `<BLANKLINE>` in the expected output with a real blank line in the actual output.

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> def a(): 
...   print()
>>> a()
<BLANKLINE>
```


## Directives

A directive comment begins with `# doctest:` after which comes a comma-separated list of options that either enable or disable various behaviors.

To enable a behavior, write a +(plus symbol) followed by the behavior name. To disable a behavior, white a – (minus symbol) followed by the behavior name.

* `+ELLIPSIS` - treat the text `...` as a wildcard that will match any text
* `+NORMALIZE_WHITESPACE` – ignore white space
* `+SKIP` – skip the test
* `+IGNORE_EXCEPTION_DETAIL`

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> 'This is expression that eval a string'
... # doctest: +ELLIPSIS
'This is ... a string'
>>> 'This is also a string' # doctest: +ELLIPSIS
'This is ... a string'
>>> import datetime as dt
>>> dt.datetime.now().isoformat() # doctest: +ELLIPSIS
'...-...-...T...:...:...'
```


🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9] # doctest: +NORMALIZE_WHITESPACE
[1, 2, 3,
4, 5, 6,
7, 8, 9]
>>> print("I will fix this later") # doctest: +SKIP
Everything is OK
>>> 1/0 # doctest: +IGNORE_EXCEPTION_DETAIL
Traceback (most recent call last):
ZeroDivisionError
```


## Trick

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def test_zero(f):
    test_str = f'\n>>> {f.__name__}()\n0\n'
    if f.__doc__:
        f.__doc__ += test_str
    else:
        f.__doc__ = test_str
    return f
    
@test_zero
def sum_nums(*args):
    "Sum func!"
    if not args:
        return 0
    return sum(args)

if __name__ == '__main__':
    import doctest
    doctest.testmod()
```
