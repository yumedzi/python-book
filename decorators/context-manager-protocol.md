# Context manager protocol

Context manager is created by defining two magic methods –` __enter__()` and `__exit__()`


```python
class Kopilka(): 
    def __init__(self, money): 
        self.money = money
    
    def __enter__(self): 
        return self.money
    
    def __exit__(self, type, value, traceback): 
        self.money = 0
    
    def go_shopping(self): 
        with self as money: 
            print("{} spent totally…:(".format(money) )
        print("{} money left".format(self.money))
        
kopilochka = Kopilka(500)
kopilochka.go_shopping() 
```

Easy way of enabling context manager protocol - via using `contextlib.contextmanager`


```python
from contextlib import contextmanager

@contextmanager
def tag(name):
    print("<%s>" % name, end="")
    yield
    print("</%s>" % name)

with tag("h1"):
    print("foo", end="")

```
Output:

    <h1>foo</h1>
