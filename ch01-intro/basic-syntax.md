# Basic syntax {#Basic-syntax}

## Identations {#Identations}

Identation or TAB, 2/4 spaces - whitespaces used to delimit program blocks - instead of punctuation or keywords, it uses indentation to indicate the run of a block.

```py
for i in [1, 2, 3]:
    if i == 3:
        print("Number 3 found!")
    else:
        print("Number:", i)
```

In C we need to use brackets\("{" and "}"\) to delimit blocks of code:

```cpp
void foo(int x)
{
    if (x == 0) {
        bar();
        baz();
    } else {
        qux(x);
        foo(x - 1);
    }
}
```

In Python the same role is after indentations which make code much easier to read:

```py
def foo(x):
    if x == 0:
        bar()
        baz()
    else:
        qux(x)
        foo(x - 1)
```

Easter egg describing the "love to braces":

```py
>>> from __future__ import braces
File "<ipython-input-1-7e6f149a161c>", line 2
    from __future__ import braces
SyntaxError: not a chance
```

Indentation must maintain the constant level for same level of nesting.

This is **correct**:

```py
if condition:
    do_something1()
    do_something2()
```

This is **incorrect**:

```py
if condition:
    do_something1()
        do_something2()
```

If code block is not big it is allowed to use inline form:

```py
if condition: do_something1()
else: do_something2()
```

And it is possible to specify few statements on the same line using`;`:

```py
a = [x for x in range(10) if x % 2]; f = open("tmp.txt", "w"); f.write(a); f.close()
```

These two examples are not readable so used very rarely.

## Identificators and reserved words {#Identificators-and-reserved-words}

Naming rules:

* can have only alphabetical characters, numbers and `_`
* can't start with number
* case sensitive
* can't be one of reserved keywords

Reserved words \(which can't be used as variable names\):

```
and       del       from      not       while    
as        elif      global    or        with     
assert    else      if        pass      yield    
break     except    import    print              
class     exec      in        raise              
continue  finally   is        return             
def       for       lambda    try
```

### Comments and documentation strings {#Comments-and-documentation-strings}

`#`- starting with this symbol everything till the end of line is ignored

```
a = 12345  # This is comment
# This is comment too
# Continuing our comments
```

Doc string - first unassigned to variable string of module, function or class. These string are used by IDEs, help auto-generating scripts etc. It is possible to specify multiline string by using starting and ending with triple quotes\(`"""`or`'''`\).

```py
def f():
    '''
    Some nice function (the best in the world)

    :no params:
    :return: None
    '''
```

```py
>>> help(f)
Help on function f in module __main__:

f()
    Some nice function (the best in the world)

    :no params:
    :return: None
```

Or:

```py
>>> f.__doc__
'\n    Some nice function (the best in the world)\n    \n    :no params:\n    :return: None\n    '
```

### Naming rules {#Naming-rules}

* Variables can only contain letters, numbers, and underscores. Variable names can start with a letter or an underscore, but can not start with a number.
* Spaces are not allowed in variable names, so we use underscores instead of spaces. For example, use student\_name instead of "student name".
* You cannot use Python keywords as variable names.
* Be careful about using the lowercase letter l and the uppercase letter O in places where they could be confused with the numbers 1 and 0.



