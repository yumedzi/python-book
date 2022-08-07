## Functools

> Standard module that provides a number of functions that operate on other functions usually returning new ones, somehow modified.

Very useful module. A sign of a good Pythonista. Most useful functions:

* partial
* **reduce**
* **wraps**
* total_ordering
* lru_cache

### functools.partial

> New function that calls target function with some arguments already set. This gives a copy of a function with less attributes.


```python
import functools, math

def string_concatenator(x, y):
    return str(x) + str(y)

helloer = functools.partial(string_concatenator, "Hello ")
byer = functools.partial(string_concatenator, y=", Bye-bye, ja nai!..")
print(helloer("World"))
print(byer("Margarita"))
### Using lambda sometimes much better:
h2 = lambda arg: string_concatenator("Hello ", arg)
print(h2("Beatufiul World"))
```

<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>Hello World
Margarita, Bye-bye, ja nai!..
Hello Beatufiul World</div>



```python
pow_of_10 = functools.partial(math.pow, 10) # 10 - first arg
pow_of_10.__doc__ = 'Bring 10 to power x'
pow_of_10(5) # 5 - second arg
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>100000.0</div>



What if we want to be able to assign specific positional argument?

It can't be done! Use `lambda` instead (of even regular `def`)


```python
quadrupler = lambda x: pow(x, 4)
quadrupler(2)
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>16</div>



It is recommended to use `lambda` instead of `functools.partial` when possible.

### functools.reduce

> Apply function of two arguments cumulatively to the items of sequence, from left to right, so as to reduce the sequence to a single value. 

> In Python 2 `functools.reduce` was builtin function `reduce`


```python
import functools
functools.reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>15</div>




```python
((((1+2)+3)+4)+5)  
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>15</div>



Factorial, "ez mode":


```python
# Reminder what is factorial:
((((1 * 2) * 3) * 4) * 5)
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>120</div>




```python
functools.reduce(lambda x, y: x * y, range(1,6))
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>120</div>




```python
from operator import mul
functools.reduce(mul, range(1,6))
```




<div style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;>120</div>



### functools.lru_cache

> Decorator to wrap a function with a memoizing callable that saves up to the maxsize most recent calls. 


```python
@functools.lru_cache(maxsize=None)
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)

print([fib(n) for n in range(20)])
print(fib.cache_info())
```

    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181]
    CacheInfo(hits=36, misses=20, maxsize=None, currsize=20)