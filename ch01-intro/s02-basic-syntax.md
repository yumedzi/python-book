# Basic syntax

## Indentations

Indentation or TAB, 2/**4 spaces** - whitespaces used to delimit program blocks - instead of punctuation or keywords, it uses indentation to indicate the run of a block.
```python
for i in [1, 2, 3]:
    if i == 3:
        print("Number 3 found!")
    else:
        print("Number:", i)
```

In C we need to use brackets(`{` and `}`) to delimit blocks of code:
```c
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

In Python the same role goes to indentations which make code much easier to read:
```python
def foo(x):
    if x == 0:
        bar()
        baz()
    else:
        qux(x)
        foo(x - 1)

```

# Easter egg describing the "love to braces"

```py
from __future__ import braces
```

```sh
SyntaxError: not a chance
```

Indentation must maintain the constant level for same level of nesting.

This is **correct**:

```python
if condition:
    do_something1()
    do_something2()
```
   
This is **incorrect**:

```python
if condition:
    do_something1()
        do_something2()
```
<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>        </code></pre>

If code block is not big it is allowed to use inline form:

```python
if condition: do_something1()
else: do_something2()
    
for x in range(x): print(x)
```

And it is possible to specify few statements on the same line using `;`:

```python
a = [x for x in range(10) if x % 2]; f = open("tmp.txt", "w"); f.write(a); f.close()
```

These two examples are not readable so used very rarely.

## Identificators and reserved words

Naming rules:
* can have only alphabetical characters, numbers and `_`
* can't start with number
* case sensitive
* can't be one of reserved keywords

Reserved words (which can't be used as variable names):

```py
and       del       from      not       while    
as        elif      global    or        with     
assert    else      if        pass      yield    
break     except    import    print     True          
class     exec      in        raise     False         
continue  finally   is        return             
def       for       lambda    try
```



### Comments and documentation strings

`#` - starting with this symbol everything till the end of line is ignored


```python
a = 12345  # This is comment
# This is comment too 
# Continuing our comments 
```

Doc string - *first string* of module, function or class. These string are used by IDEs, help auto-generating scripts etc. It is possible to specify multiline string by using starting and ending with triple quotes(`"""` or `'''`).


```python
def f():
    '''
    Some nice function (the best in the world)
    
    :no params:
    :return: None
    '''

help(f)
```

<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Help on function f in module __main__:</code></pre>
    
    f()
        Some nice function (the best in the world)
        
        :no params:
        :return: None
    


Or:


```python
f.__doc__
```

### Naming rules

* Variables can only contain letters, numbers, and underscores. Variable names can start with a letter or an underscore, but can not start with a number.
* Spaces are not allowed in variable names, so we use underscores instead of spaces. For example, use student_name instead of "student name".
* You cannot use Python keywords as variable names.
* Be careful about using the lowercase letter l and the uppercase letter O in places where they could be confused with the numbers 1 and 0.