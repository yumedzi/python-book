# Builtins

> There are lot of builtin functions (no need to import them) that are always available.

> https://docs.python.org/3/library/functions.html

Some example that we already saw: 
* `print()`
* `len()`
* `pow()`
* `int()`
* `str()`
* `type()`
* `isinstance()`
* `range()`
* `sum()`, `max()`, `min()`, `enumerate()`, `round()`...

But there are much more of them!

<table border="1" class="docutils">
<thead valign="bottom">
<tr class="row-odd">
<th class="head" colspan=5><center>Built-in Functions</center></th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td>abs()</td>
<td>dict()</td>
<td>help()</td>
<td>min()</td>
<td>setattr()</td>
</tr>
<tr class="row-odd"><td>all()</td>
<td>dir()</td>
<td>hex()</td>
<td>next()</td>
<td>slice()</td>
</tr>
<tr class="row-even"><td>any()</td>
<td>divmod()</td>
<td>id()</td>
<td>object()</td>
<td>sorted()</td>
</tr>
<tr class="row-odd"><td>ascii()</td>
<td>enumerate()</td>
<td>input()</td>
<td>oct()</td>
<td>staticmethod()</td>
</tr>
<tr class="row-even"><td>bin()</td>
<td>eval()</td>
<td>int()</td>
<td>open()</td>
<td>str()</td>
</tr>
<tr class="row-odd"><td>bool()</td>
<td>exec()</td>
<td>isinstance()</td>
<td>ord()</td>
<td>sum()</td>
</tr>
<tr class="row-even"><td>bytearray()</td>
<td>filter()</td>
<td>issubclass()</td>
<td>pow()</td>
<td>super()</td>
</tr>
<tr class="row-odd"><td>bytes()</td>
<td>float()</td>
<td>iter()</td>
<td>print()</td>
<td>tuple()</td>
</tr>
<tr class="row-even"><td>callable()</td>
<td>format()</td>
<td>len()</td>
<td>property()</td>
<td>type()</td>
</tr>
<tr class="row-odd"><td>chr()</td>
<td>frozenset()</td>
<td>list()</td>
<td>range()</td>
<td>vars()</td>
</tr>
<tr class="row-even"><td>classmethod()</td>
<td>getattr()</td>
<td>locals()</td>
<td>repr()</td>
<td>zip()</td>
</tr>
<tr class="row-odd"><td>compile()</td>
<td>globals()</td>
<td>map()</td>
<td>reversed()</td>
<td>__import__()</td>
</tr>
<tr class="row-even"><td>complex()</td>
<td>hasattr()</td>
<td>max()</td>
<td>round()</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd"><td>delattr()</td>
<td>hash()</td>
<td>memoryview()</td>
<td>set()</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>

## Most important builtins
* Types are callable:
    * `int()`
    * `float()`
    * `str()`
    * `list()`
    * `dict()`
    * `set()`
    * `bool()`
    * `frozenset()`
    

* Introspection:
    * `id()`
    * `dir()`
    * `type()`
    * `isinstance()`
    * `issubclass()`
    * `callable()`
    * `hash()`
    * `help()`

* `__import__()`
* `len()`, `print()`
* `abs()`, `sum()`, `max()`, `min()`,  `pow()`, `round()`
* `range()`, `sorted()`, `reversed()`, `enumerate()`, `all()`, `any()`
* `open()`
* `globals()`, `locals()`, (not builtins but don't forget about: `global`, `nonlocal`)

## Access to object attributes

* `getattr(obj, "attr_name"[, default])`

* `hasattr(obj, "attr_name")`

* `setattr(obj, "attr_name", value)`

* `delattr(obj, "attr_name")`
 


🪄 _<mark style="color:red;">Code</mark>_:

```python
class A(object):
    a = 5
    
a_object = A()
print( hasattr(a_object, "a") )
print( getattr(a_object, "a") )
setattr(a_object, "b", "Wow! Adding attrs like haxxxors")
print( a_object.b )
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
True
5
Wow! Adding attrs like haxxxors
```
{% endcode %}
🪄 _<mark style="color:red;">Code</mark>_:

```python
getattr("Hello World", "lower")()
```




📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
'hello world'
```
{% endcode %}
# Iterable and Iterator

> **Iterable** is the source of data for iterator, usually - some sequence.

```python
[1, 2, 3]
("a", "b")
"Hello!"
{1: 2, "a": 3}
{1, 2, 3}
range(10)
reversed("abc")
```

> **Iterator** - an abstract object that is capable of yielding "next" item and raising `StopIteration` in the end.

```python
iter("abce")

next(iter("abce"))
iter("abce").__next__()

for i in "abcd":
    print(i)
```