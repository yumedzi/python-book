# Riddle decorator example

To check your understanding of decorator to this point - try to explain what the following decorator does.

* What the purpose of riddle_deco?
* Is there any issues in riddle_deco?

Hints:
* remember counter decorator!


```python
def riddle_deco(f):
    def _f(bill, *args):
        if not hasattr(_f, "_val"):
            _f._val = dict()
        
        if not bill in _f._val:
            _f._val[bill] = f(bill, *args)
        return _f._val[bill]

    return _f

@riddle_deco
def calc_tips(bill, tip_rate=0.10):
    return int(bill * tip_rate)
```


```python
>>> calc_tips(100)
10

>>> calc_tips(200, 0.05)
10

>>> calc_tips(100, 0.05) # Surprise! Why?
10

>>> calc_tips._val
{100: 10, 200: 10}
```    

Way to improve this cashing decorator - change key to a tuple that contains a `tip_rate` also. In this way we'll cover all possible cases.


```python
def riddle_deco(f):
    def _f(bill, tip_rate=0.10, *args):
        if not hasattr(_f, "_val"):
            _f._val = dict()
        
        if not (bill, tip_rate) in _f._val:
            _f._val[bill, tip_rate] = f(bill, tip_rate, *args)
        return _f._val[bill, tip_rate]

    return _f

@riddle_deco
def calc_tips(bill, tip_rate=0.10):
    return int(bill * tip_rate)
```
