# What is left behind?

* [itertools](https://docs.python.org/3/library/itertools.html)
    + Number of various "batteries" providing most imaginable iterators for most usecases
* [operator](https://docs.python.org/3/library/operator.html)
    + efficient functions corresponding to the intrinsic operators of Python. For example, `operator.add(x, y)` is equivalent to the expression `x+y`.
* coroutines
    + generators that can get value via yield:
    ```python
    val = (yield i)
    ```

Example of coroutine:

```python
def pluser():
    val = 0
    while True:
       val = (yield val) + 1
p = pluser()
print(p.send(None)) # p.__next__()
print(p.send(10))
print(p.send(-25.3))
```
Output:

    0
    11
    -24.3