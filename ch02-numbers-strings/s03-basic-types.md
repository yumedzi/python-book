## Basic types of objects in Python

| Category    | Explanation                                  | Types|
|--|--|---|
| Mutable                | Object can be changed after creation                   | `list, dict, set, bytearray`                   |
| Immutable              | Object can not be changed after creation               | `int, float, complex, str, tuple, frozenset`        |
| Sequence (collection, iterable)  | Object can holds other object in itself (has magic methods like `__getitem__()`) |    `list, tuple, set, str, frozenset, dict` |
| Ordered| Members are ordered | `list`, `str`, `tuple`, `dict` |
| Unordered | Members are unordered | `set`, `frozenset` |

### Additional categories:
| Category    | Explanation | Types|
|--|--|---|
| Hashable               | Object that can be a key to dictionary (has `__hash__()` - all immutable and instances of custom classes) | `tuple, int, float, str, frozenset, object` |
| Iterable               | Object capable of returning it's member one at a time (has `__iter__()` or `__getitem__()`)  | `str, list, tuple, set, frozenset, dict` |
| Callable               | Object that can behave as function (has `__call__()` method defined) | `class`, `function`, `method`

## Basic types

<span title="This is important" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">ℹ️</span>

| Type        | Name         | Short description                        | Mutable | Example            |
|-------------|--------------|------------------------------------------|---------|---------------------------
| `NoneType`  | None         | "Empty" value                            | No    |  `None`               |
| `bool`      | Boolean      | Boolean value  (`True` or `False`)       | No    |  `True`               | 
| `int`       | Integer      | Integer numbers                          | No    |  `42`                 |
| `float`     | Float        | Floating point number                    | No    |  `23.43`              |
| `str`       | String       | Textual data - sequense of characters    | No    |  `"Hello!"`           |
| `list`      | List         | Mutable sequense of any kind of objects  | Yes   |  `[1, 2, 3]`          |
| `tuple`     | Tuple        | Immutable sequense of objects            | No    |  `(1, 2, 3)`          |
| `set`       | Set          | Mutable collection of unique objects     | Yes   |  `{1, 2, 3}`          |
| `frozentset`| Frozen Set   | Immutable collection of unique objects   | No    |  `frozenset({1, 2, 3})`          |
| `dict`      | Dictionary   | The collection of key-value pairs        | Yes   |  `{"name": "Johnny", "second_name": "Walker" }`  |
|   

Main categories:
* Mutable or Immutable
    * Is object allowing it's change after creation?
* Hashable
    * Can this object be used as the key for the dictionary (has defined `__hash__()` and `__eq__()` methods)?
* Container, sequence, iterable
    * Has this object contained elements like other objects (has methods like `__iter__` or `__getitem__()`)?
* Callable
    * Can be invoked/run like a function or class (has method `__call__()` defined)? 

Additional types:
* `function` 
* `code object`
* `module`
* `iterator`
* `generator`
* `slice object`

And much more (because everything in Python is a object and thus - everything is of some specific type).

### Sizes of the object of basic types:

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>


🪄 _<mark style="color:green;">Code:</mark>_

```python
import sys, rich

table = rich.table.Table(rich.table.Column(header="Object", style="blue"), 
                         "Type", 
                         rich.table.Column(header="Size", style="cyan", justify="right"),
                         title="Basic types memory usage", show_lines=True)
objects = [ None, True, 42, 3.1415, "Hello", [1, 2, 3], ("a", "b", "c"),
            {1, 2, 3}, frozenset({1, 2, 3}), {"x": 1, "y": 2} ]

for obj in objects:
    table.add_row(*map(str, (obj, type(obj), sys.getsizeof(obj))))
rich.console.Console().print(table)
```


📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
---------------------------------------------------------------------------

ModuleNotFoundError                       Traceback (most recent call last)

Input In [8], in <cell line: 1>()
----> 1 import sys, rich
      3 table = rich.table.Table(rich.table.Column(header="Object", style="blue"), 
      4                          "Type", 
      5                          rich.table.Column(header="Size", style="cyan", justify="right"),
      6                          title="Basic types memory usage", show_lines=True)
      7 objects = [ None, True, 42, 3.1415, "Hello", [1, 2, 3], ("a", "b", "c"),
      8             {1, 2, 3}, frozenset({1, 2, 3}), {"x": 1, "y": 2} ]


ModuleNotFoundError: No module named 'rich'
```
{% endcode %}
<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Memory requirement to store elements of `int` type in a different collections.

For _1 million_ of elements:

| Type | Bytes per element |
|------|-----------
| Tuple |8
| List  |9
| Set   | 33
| Dictionary | 42

Memory size may not be the only criteria to select data type. Rather, time required to perform operation on data type can be critical criteria.


🪄 _<mark style="color:green;">Code:</mark>_

```python
import sys, rich
n = 1000000

tests = {
    "list": [*range(n)],
    "tuple": tuple(range(n)),
    "set": set(range(n)),
    "dict": dict.fromkeys(range(n))
}

table = rich.table.Table("Type", 
                         rich.table.Column(header="Total size", style="cyan", justify="right"), 
                         rich.table.Column(header="Size per element", style="red", justify="right"),
    title=f"Collections memory requirement ({n} elements)", show_lines=True
)
for type_, collection in tests.items():
#     print(f"Size of <{type_}> ({n} items): {sys.getsizeof(collection)}, {sys.getsizeof(collection) / n} per element")
    table.add_row(str(type_), str(sys.getsizeof(collection)), str(sys.getsizeof(collection) / n))
rich.console.Console().print(table)
```


📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
---------------------------------------------------------------------------

ModuleNotFoundError                       Traceback (most recent call last)

Input In [9], in <cell line: 1>()
----> 1 import sys, rich
      2 n = 1000000
      4 tests = {
      5     "list": [*range(n)],
      6     "tuple": tuple(range(n)),
      7     "set": set(range(n)),
      8     "dict": dict.fromkeys(range(n))
      9 }


ModuleNotFoundError: No module named 'rich'
```
{% endcode %}
