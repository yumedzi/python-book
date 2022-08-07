# Functions internals

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Function is wrapper around code object. Code object is wrapper for byte-code.


```python
def f1():
    return "Hello"
f2 = lambda: "Hello"

print(f1.__code__.co_code)
print(f2.__code__.co_code)
```

<pre class="notranslate" style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>b'd\x01S\x00'
    b'd\x01S\x00'</code></pre>



```python
print(f1.__code__.__doc__)
```

<pre class="notranslate" style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>code(argcount, kwonlyargcount, nlocals, stacksize, flags, codestring,
          constants, names, varnames, filename, name, firstlineno,
          lnotab[, freevars[, cellvars]])</code></pre>
    
    Create a code object.  Not for the faint of heart.