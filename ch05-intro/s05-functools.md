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


🪄 _<mark style="color:green;">Code:</mark>_

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

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Hello World
Margarita, Bye-bye, ja nai!..
Hello Beatufiul World
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
pow_of_10 = functools.partial(math.pow, 10) # 10 - first arg
pow_of_10.__doc__ = 'Bring 10 to power x'
pow_of_10(5) # 5 - second arg
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
100000.0
```
{% endcode %}
What if we want to be able to assign specific positional argument?

It can't be done! Use `lambda` instead (of even regular `def`)


🪄 _<mark style="color:green;">Code:</mark>_

```python
quadrupler = lambda x: pow(x, 4)
quadrupler(2)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
16
```
{% endcode %}
It is recommended to use `lambda` instead of `functools.partial` when possible.

### functools.reduce

> Apply function of two arguments cumulatively to the items of sequence, from left to right, so as to reduce the sequence to a single value. 

> In Python 2 `functools.reduce` was builtin function `reduce`


🪄 _<mark style="color:green;">Code:</mark>_

```python
import functools
functools.reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
15
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
((((1+2)+3)+4)+5)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
15
```
{% endcode %}
Factorial, "ez mode":


🪄 _<mark style="color:green;">Code:</mark>_

```python
# Reminder what is factorial:
((((1 * 2) * 3) * 4) * 5)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
120
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
functools.reduce(lambda x, y: x * y, range(1,6))
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
120
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
from operator import mul
functools.reduce(mul, range(1,6))
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
120
```
{% endcode %}

### functools.lru_cache

> Decorator to wrap a function with a memoizing callable that saves up to the maxsize most recent calls. 


🪄 _<mark style="color:green;">Code:</mark>_

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