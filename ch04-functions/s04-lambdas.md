# Anonymous functions

> Anonymous function also known as lambdas after operator which creates them.

> Lambda expressions are a way to define a function inline in runtime without a def statement

* No return, just one single expression
* ```def``` vs ```lambda``` – lambda creates and returns function object, def creates and binds the function to the name
* Not faster
* They are needed when you want to pass callable object or process something only once.

```python
lambda [arg1 [,arg2,.....argn]]: <expression>
```

* Lambdas can take any number of arguments but return just one value in the form of an expression. 
* They cannot contain commands or multiple expressions. 
* An anonymous function cannot be a direct call to print because lambda requires an expression 
* Used a lot in functional programming where you can pass functions to other functions

Why lambda?

* The lambdas can be used as a function shorthand that allows us to embed a function within the code. 
    * key in `sorted`
    
🪄 _<mark style="color:green;">Code:</mark>_

```python
sorted([1, 2, "a", (3, 4)], key=lambda x: str(x))
sorted([1, 2, 11, 3, "11", "asd", "5"], key=lambda x: f"{x:>10}")
```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```

```
{% endcode %}

* For example, callback handlers are frequently coded as inline lambda expressions embedded directly in a registration call's arguments list. Instead of being define with a `def` elsewhere in a file and referenced by name
    
* Lambdas are also commonly used to code jump tables which are lists or dictionaries of actions to be performed on demand.


🪄 _<mark style="color:green;">Code:</mark>_

```python
f = lambda x, y: x + y 
f(2, 6)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
8
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
list(map(lambda x: x**2, range(5)))
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[0, 1, 4, 9, 16]
```
{% endcode %}

```python
def power_n(n): 
    import math 
    return lambda x: math.pow(x, n) 
print(power_n(3)(3))
squared = power_n(4)
print(squared(5))
```

### Example from production

```python
conversions = {
            "ram"                    : lambda a, v, m, o: memory.normalizeRam(v),
            "logical_ram"            : lambda a, v, m, o: memory.normalizeRam(v),
            "processor_type"         : lambda a, v, m, o: None,
            "num_processors"         : lambda a, v, m, o: None,
            "num_logical_processors" : lambda a, v, m, o: None,
            "uptime"                 : convertUptime,
            "uptimeSeconds"          : intConvert,
    }
```

## Performance of lambda vs regular function

The same.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def f1():
    return len([ x for x in range(10000)])

f2 = lambda: len([ x for x in range(10000)])

%timeit f1()
%timeit f2()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
654 µs ± 13.6 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
663 µs ± 9.15 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```
{% endcode %}

This is because lambda is syntax sugar and in the end almost the same code is being constructed


🪄 _<mark style="color:green;">Code:</mark>_

```python
import dis
dis.dis(f1)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
  2           0 LOAD_GLOBAL              0 (len)
              3 LOAD_CONST               1 (<code object <listcomp> at 0x103e14c90, file "<ipython-input-67-9c2575e1edb3>", line 2>)
              6 LOAD_CONST               2 ('f1.<locals>.<listcomp>')
              9 MAKE_FUNCTION            0
             12 LOAD_GLOBAL              1 (range)
             15 LOAD_CONST               3 (10000)
             18 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
             21 GET_ITER
             22 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
             25 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
             28 RETURN_VALUE
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
dis.dis(f2)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
  4           0 LOAD_GLOBAL              0 (len)
              3 LOAD_CONST               1 (<code object <listcomp> at 0x103e149c0, file "<ipython-input-67-9c2575e1edb3>", line 4>)
              6 LOAD_CONST               2 ('<lambda>.<locals>.<listcomp>')
              9 MAKE_FUNCTION            0
             12 LOAD_GLOBAL              1 (range)
             15 LOAD_CONST               3 (10000)
             18 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
             21 GET_ITER
             22 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
             25 CALL_FUNCTION            1 (1 positional, 0 keyword pair)
```
{% endcode %}

                 28 RETURN_VALUE