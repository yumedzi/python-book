# Functions internals \*

Function is wrapper around code object. Code object is wrapper for byte-code.


```python
def f1():
    return "Hello"
f2 = lambda: "Hello"

print(f1.__code__.co_code)
print(f2.__code__.co_code)
```
Output:

    b'd\x01S\x00'
    b'd\x01S\x00'


It is possible to create function from byte-code, there is the help for code object constructor:

```python
help(f1.__code__)
```
Output (mind "Not for the faint of heart" part):

    code(argcount, kwonlyargcount, nlocals, stacksize, flags, codestring,
          constants, names, varnames, filename, name, firstlineno,
          lnotab[, freevars[, cellvars]])
    
    Create a code object.  Not for the faint of heart.

