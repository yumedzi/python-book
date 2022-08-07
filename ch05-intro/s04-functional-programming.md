# Functional Programming

Main styles of programming / paradigms:

* Imperative Programming (IP) = computation in terms of statements that change a program state from initial to result

* Object-oriented Programming (OOP) = computation based on manipulation on collections of objects. Objects have internal state and support methods that query or modify this internal state in some way.
 
* Declarative Programming (DP) = expressing the logic of a computation without describing its control flow

    * Functional Programming (FP) = computation as the evaluation of mathematical functions and avoids state and mutable data apply transformation (and compositions)


In other words:

* Imperative Programming
    * a sequence of steps/instructions that happen in order (some algorithm) to calculate needed result

* Functional Programming
    * a set of functions that transform data into needed result

Per language:

* Imperative programming
    * C, C++
    * Pascal
    * Basic, Sh
    * Python
* OOP
    * Java
    * Smalltalk
    * C++
    * Python

* Declarative programming
    * Functional programming
        * Haskell
        * Scheme
        * OCaml
        * Python
    * Logic programming (Prolog, Clojure core.logic)


> Python is flexible allowing most programming styles

What is mostly used in Imperative Programming paradigm:

* while statements
* for loops
* functions
* assignments and changing variables

How Functional Programming is different:

* loops -> recursion, `map`, `filter`, `reduce`, comprehensions
* changing variables -> no changing variables once set, instead - immutable types: `tuple`, `frozenset`
* functions -> return value is only dependent on this function's input 

```py
def imp_function():
    res = 0
    do_this()
    do_that()
    do_and_that()
    print(res)
```

```py
def fp_function(data):
    return do_and_that(do_that(do_this(data)))
```

```py
def imp_function():
    res = 0
    a = data.split()
    for x in a:
        res += int(x)
    print(res)
```

```py
def fp_function(data):
    return sum(map(int, data.split()))
```

Abstract and not abstract examples:

|Imperative|Functional|
|----------------|--------------------------|
|<pre>def imp_function():<br/>    res = 0<br/>    do_this()<br/>    do_that()<br/>    do_and_that_also()<br/>    print(res)<br/></pre>|<pre>def fp_function(data):<br/>    return do_and_that_also(do_that(do_this(data)))<br/></pre>|
|<pre>def imp_function():<br/>    res = 0<br/>    a = data.split()<br/>    for x in a:<br/>        res += int(x)<br/>    print(res)</pre>|<pre>def fp_function(data):<br/>    return sum(map(int, data.split()))<br/></pre>|


Task:

> Evaluate expression ignoring some mistakes:

> `"1+2+22+++100++48"`

> We need to calculate in this manner: 1+2+22+100+48

## Imperative approach


```python
expr = "1+2+22+++100++48"
res = 0

for t in expr.split("+"):
    if t != "":
        res += int(t)
print( res ) 
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
173
{% endcode %}



## Functional approach


🪄 _<mark style="color:green;">Code:</mark>_

```python
sum(map(int, filter(bool, expr.split("+"))))
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
173
{% endcode %}




Don't freak out - we'll cover all of this.

One more example that shows how different reading of some code weritten via imperative programming style or functional is.

Let's try to guess quickly what the following two functions do.

Imperative:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def mystery_imp(x):
    r = 0
    for c in x:
        cl = c.lower()
        if cl == "a" or cl == "b" or cl == "c":
            r += 1
    return r
```

Functional:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def mystery_fp(str_):
    return len(list(filter(lambda x: x.lower() in "abc", str_)))
```

Yes, both of them are case-insensitively counting `'a'`, `'b'` and `'c'` characters in a string:


🪄 _<mark style="color:green;">Code:</mark>_

```python
str_ = "A beautiful example of some test string"
print(mystery_imp(str_))
print(mystery_fp(str_))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
4
4
{% endcode %}



Functional is a bit easier to understand...

## Map

> `map(function, iterable1, iterable2, ..., iterableN)` 

> Return an iterator that computes the function using arguments from each of the iterables.  Stops when the shortest iterable is exhausted. 

On Python 2 - map returns list.

For Python 3 sometimes it's better to use list comprehensions


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(list(map(str, [1, 2, 3])))
print(list(map(pow, [2, 5], [3, 4])))
print(list(map(lambda x,y: x**2 + 2*x*y + y**2, range(10)[::-1], [10]*10)))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
['1', '2', '3']
[8, 625]
[361, 324, 289, 256, 225, 196, 169, 144, 121, 100]
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
print([str(x) for x in [1, 2, 3]])
print([pow(x[0], x[1]) for x in zip([2, 5], [3, 4])])
print([pow(x, y) for x,y in zip([2, 5], [3, 4])])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
['1', '2', '3']
[8, 625]
[8, 625]
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
print(list(map(sum, [[1, 2, 3] , [4, 5, 8]])))
print(list(map(lambda x: x+1, [1, 2, 3])))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
[6, 17]
[2, 3, 4]
{% endcode %}



## Filter

> `filter(function, iterable)`

> Construct an iterator from those elements of iterable for which function returns `True`


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(list(filter(bool, [1, 2, 0])))
print(list(filter(lambda x: x > 0, [-2, -1, 0, 1, 2])))
print(list(filter(lambda x: x%2, [1, 2, 3, 4, 5, 6, 7, 8])))
print(list(filter(lambda z: int(z) % 2 if isinstance(z, int) else True, [1,2,3,4,5,0, "a", [], 0.0, False, None])))
print(list(filter(lambda z: int(z) % 2 if isinstance(z, int) else False, [1,2,3,4,5,0, "a", [], 0.0, False, None])))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
[1, 2]
[1, 2]
[1, 3, 5, 7]
[1, 3, 5, 'a', [], 0.0, None]
[1, 3, 5]
{% endcode %}



## Zip

> `zip(*iterables)`

> Make an iterator that aggregates elements from each of the iterables.

Simply speaking `zip()` creates pairs from elements of provided arguments 


```python
print(list( zip([1, 3], [2, 4] )))
print(list( zip([1, 2, 3, 4], [1, 2, 0]) ))
# Unzipping
zipped = zip([1, 2, 3, 4], [1, 2, 0])
print(list( zip(*zipped) )) # Note that we'll loose element from longer list
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
[(1, 2), (3, 4)]
[(1, 1), (2, 2), (3, 0)]
[(1, 2, 3), (1, 2, 0)]
{% endcode %}



## Other perls of FP

* Avoid state 
* Immutable data 
* First-class functions 
* Higher-order functions 
* Pure functions 
* Recursion, tail recursion 
* Iterators, sequences, lazy evaluation, pattern matching, monads...