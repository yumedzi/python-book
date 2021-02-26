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

### Examples of basic types

| Type | Example            |
|------|--------------------|
| `NoneType`     | `None`               |
| `int`      | `42`                 |
| `bool`     | `True`               |
| `float`    | `23.43`              |
| `str`      | `"Hello!"`           |
| `list`     | `[1, 2, 3]`          |
| `tuple`    | `(1, 2, 3)`          |
| `set`      | `{1, 2, 3}`          |
| `dict`     | `{"name": "Johnny", "second_name": "Walker" }`  |


Additional types (to check for these type use `types` module):
* `function` 
* `code object`
* `module`
* `iterator`
* `generator`
* `slice object`