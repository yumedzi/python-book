# Functions internals

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Function is wrapper around code object. Code object is wrapper for byte-code.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def f1():
    return "Hello"
f2 = lambda: "Hello"

print(f1.__code__.co_code)
print(f2.__code__.co_code)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'd\x01S\x00'
b'd\x01S\x00'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
print(f1.__code__.__doc__)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
code(argcount, kwonlyargcount, nlocals, stacksize, flags, codestring,
      constants, names, varnames, filename, name, firstlineno,
      lnotab[, freevars[, cellvars]])

Create a code object.  Not for the faint of heart.
```
{% endcode %}
