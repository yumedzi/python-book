# Classification of basic types

There is a number of classifications of basic types. Main one - mutable/immutable but it is good to know others to distinguish them and to use common methods for similar types.

## Basic types of objects in Python {#Basic-types-of-objects-in-Python-1.5}

| Category | Explanation | Types |
| :--- | :--- | :--- |
| Mutable | Object can be changed after creation | `list, dict, set` |
| Immutable | Object can not be changed after creation | `int, float, str, tuple, frozenset` |
| Sequence \(collection\) | Object can holds other object in itself \(has magic methods like `__getitem__()`\) | `list, tuple, set, str, frozenset, dict` |
| Ordered | Members are ordered | list, str, tuple |
| Unordered | Members are unordered | dict, set, frozenset |

### Additional categories: {#Additional-categories:-1.5.1}

| Category | Explanation | Types |
| :--- | :--- | :--- |
| Hashable | Object that can be a key to dictionary \(has`__hash__()`- all immutable and instances of custom classes\) | `tuple, int, str, frozenset, object` |
| Iterable | Object capable of returning it's member one at a time \(has`__iter__()`or`__getitem__()`\) | `str, list, tuple, set, frozenset, dict` |
| Callable | Object that can behave as function \(has`__call__()`method defined\) | class, function, method |

### Examples of basic types {#Examples-of-basic-types-1.5.2}

| Type | Example |
| :--- | :--- |
| `None` | `None` |
| `int` | `42` |
| `float` | `23.43` |
| `str` | `"Hello!"` |
| `list` | `[1, 2, 3]` |
| `tuple` | `(1, 2, 3)` |
| `set` | `{1, 2, 3}` |
| `frozenset` | `frozenset({1, 2, 3, 4})` |
| `dict` | `{"name": "Johnny", "second_name": "Walker" }` |

Additional types:

* `function`
* `code object`
* `module`
* `iterator`
* `generator`
* `slice object`



