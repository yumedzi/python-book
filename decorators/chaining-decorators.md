# Chaining decorators

It is possible to chain and use multiple decorators in succession.


```python
def makebold(fn): 
    def wrapped(*args, **kwargs): 
        return "<b>" + str(fn(*args, **kwargs)) + "</b>" 
    return wrapped

def makeitalic(fn): 
    def wrapped(*args, **kwargs): 
        return "<i>" + str(fn(*args, **kwargs)) + "</i>" 
    return wrapped

def makered(fn): 
    def wrapped(*args, **kwargs): 
        return "<span style='color: red;'>" + str(fn(*args, **kwargs)) + "</span>"
    return wrapped

```

Example of usage:

```python
@makebold
@makeitalic
@makered
def hello(text="Goodbye World!"):
    return text

hello() 
```

Output:


    "<b><i><span style='color: red;'>Goodbye World!</span></i></b>"

The trick for underderstanding this is that chained decorators above are the same as the following code:

```python
def hello(text="Goodbye World!"):
    return text

hello = makebold(makeitalic(makered(hello)))
```

It is possible to chain decorators in any combination needed:

```python
@makebold
@makeitalic   
@makebold 
@makebold
def hello(text="Goodbye again, World!"):
      return text

hello() 
```

Output:


    '<b><i><b><b>Goodbye again, World!</b></b></i></b>'



As resume memoization rule:
    
> Decorator is 

> * `function`

>     * that takes `function` as argument and returns

>        * `function`

