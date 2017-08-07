# Functools

> Standard module that provides a number of functions that operate on other functions usually returning new ones, somehow modified.

Very useful module. A sign of a good Pythonista. Most useful functions:

* partial
* reduce
* wraps
* total_ordering
* lru_cache

## functools.partial

> Return a new partial object which when called will behave like func called with the positional arguments args and keyword arguments keywords


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
Output:

    Hello World
    Margarita, Bye-bye, ja nai!..
    Hello Beatufiul World
    


```python
pow_of_10 = functools.partial(math.pow, 10) # 10 - first arg
pow_of_10.__doc__ = 'Bring 10 to power x'
pow_of_10(5) # 5 - second arg
```
Output:

    100000.0



What if we want to be able to assign specific positional argument?

It can't be done! Use lambda instead


```python
>>> quadrupler = lambda x: math.pow(x, 4)
>>> quadrupler(3)
81.0
```


## functools.reduce

> Apply function of two arguments cumulatively to the items of sequence, from left to right, so as to reduce the sequence to a single value. 

> In Python 2 `functools.reduce` was builtin function `reduce`


```python
>>> functools.reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])
15
```

```python
((((1+2)+3)+4)+5)  
15
```

Factorial, "ez mode":

```python
# Reminder what is factorial: 
>>> 1 * 2 * 3 * 4 * 5
120
```

```python
>>> functools.reduce(lambda x,y: x * y, range(1,6))
120
```

```python
>>> from operator import mul
>>> functools.reduce(mul, range(1,6)) 
120
```

## functools.lru_cache

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
Output:

    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181]
    CacheInfo(hits=36, misses=20, maxsize=None, currsize=20)
    
