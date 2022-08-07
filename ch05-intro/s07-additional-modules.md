# What is left behind?

* itertools
    + Number of various "batteries" providing most imaginable iterators for most usecases
* operator
    + I've shown example of `operator.mul`. There are lot of similar functions providing functionality of main operators
* coroutines *
    + generators that can get value via yield:
    ```python
    val = (yield i)
    ```


```python
def pluser():
    val = 0
    while True:
       val = (yield val) + 1

p = pluser()
print(p)
#print(next(p))
print(p.send(None)) # p.__next__()
print(p.send(10))
print(p.send(-25.3))
```

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code><generator object pluser at 0x7f4b14319a20>
    0
    11</code></span>
    -24.3