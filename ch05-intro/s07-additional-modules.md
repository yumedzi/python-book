# What is left behind?

* [itertools](https://docs.python.org/3/library/itertools.html)
    + Number of various "batteries" providing most imaginable iterators for most usecases
* [operator](https://docs.python.org/3/library/operator.html)
    + I've shown example of `operator.mul`. There are lot of similar functions providing functionality of main operators
* coroutines *
    + generators that can get value via yield:
    ```python
    val = (yield i)
    ```


🪄 <mark style="color:red;">Code</mark>:

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

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<generator object pluser at 0x7f4b14319a20>
0
11
-24.3
```
{% endcode %}
