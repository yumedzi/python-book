# Functional Programming

Main styles of programming / paradigms:

* Imperative Programming (IP) = computation in terms of statements that change a program state actions that change state from initial state to result

* Object-oriented Programming (OOP) = computation based on manipulation on collections of objects. Objects have internal state and support methods that query or modify this internal state in some way.
 
* Declarative Programming (DP) = expressing the logic of a computation without describing its control flow

    * Functional Programming (FP) = computation as the evaluation of mathematical functions and avoids state and mutable data apply transformation (and compositions)


Examples:

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
        * Haskell, 
        * Scheme, 
        * OCaml
        * Python
    * Logic programming (Prolog, Clojure core.logic)


> Python is flexible allowing most programming styles

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
Output:

    173
    

## Functional approach


```python
sum(map(int, filter(bool, expr.split("+"))))
173
```

Don't freak out - we'll cover all of this.

## Map

> `map(function, iterable1, iterable2, ..., iterableN)` 

> Return an iterable that computes the function using arguments from each of the iterables.  Stops when the shortest iterable is exhausted. 

On Python 2 - map returns list.

For Python 3 sometimes it's better to use list comprehensions


```python
print(list(map(str, [1, 2, 3])))
print(list(map(pow, [2, 5], [3, 4])))
print(list(map(lambda x,y: x*y, range(10)[::-1], [1223]*34)))
```
Output:


    ['1', '2', '3']
    [8, 625]
    [11007, 9784, 8561, 7338, 6115, 4892, 3669, 2446, 1223, 0]
    


```python
print([str(x) for x in [1, 2, 3]])
print([pow(x[0], x[1]) for x in zip([2, 5], [3, 4])])
```
Output:


    ['1', '2', '3']
    [8, 625]
    


```python
print(list(map(sum, [[1, 2, 3] , [4, 5, 8]])))
print(list(map(lambda x: x+1, [1, 2, 3])))    
```
Output:

    [6, 17]
    [2, 3, 4]
    

## Filter

> `filter(function, iterable)`

> Construct an iterator from those elements of iterable for which function returns `True`


```python
print(list(filter(None, [1, 2, 0])))
print(list(filter(lambda x: x > 0, [-2, -1, 0, 1, 2])))
print(list(filter(lambda x: not x%2, [1, 2, 3, 4, 5, 6, 7, 8])))
```
Output:

    [1, 2]
    [1, 2]
    [2, 4, 6, 8]
    

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
Output:

    [(1, 2), (3, 4)]
    [(1, 1), (2, 2), (3, 0)]
    [(1, 2, 3), (1, 2, 0)]
    

## Other perls of FP

* Avoid state 
* Immutable data 
* First-class functions 
* Higher-order functions 
* Pure functions 
* Recursion, tail recursion 
* Iterators, sequences, lazy evaluation, pattern matching, monads...