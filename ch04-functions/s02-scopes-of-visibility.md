# Namespaces

Namespaces are just dictionaries with some names (what we call variable name) mapped to objects (actual data in memory). This mapping allows to access target object by a name that we've assigned to it. So: 
```python
some_string = "Hello World"
```
creates a reference to the "Hello Worold" object, and makes it accessible by variable name ```some_string```.

In this case our namespace will be:
```python
{"some_string": "Hello World"}
```

In Python it's possible to have multiple namespaces (for example: each function has it's own context). When we trying to get some variable inside some namespace Python firstly looks at so-called local namespace and if it is not found it goes "upper". Such local contextual namespaces in Python called "scopes".

## Scopes of visibility

> All variables in a program may not be accessible at all locations in that program. This depends on where you have declared a variable. 

> The scope of a variable determines the portion of the program where you can access a particular identifier. 

Scopes of visibility in Python:
* Builtin variables
* Global variables
* Enclosed variables
* Local variables

The search is goes only in those 4 places!

<img src="../images/scope_resolution_1.png">

Local variables can be accessed only inside the function in which they are declared, whereas global variables can be accessed throughout the program body by all functions. When you call a function, the variables declared inside it are brought into scope. Use ```global```to access global variable.

If a name is bound in a block, it is a **local variable** of that block, unless declared as `nonlocal` or `global`. If a name is bound at the module level, it is a **global variable**. (The variables of the module code block are local and global.) If a variable is used in a code block but not defined there, it is a **free variable**.


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("builtin:", all)
all = [1, 2, 3]
print("global:", all)
def foo():
    all = [4, 5, 6]
    
    def inner1():
        nonlocal all 
        all = [1, 2, 3, "changed!"]
        print("enclosed:", all)
        
    def inner2():
        global all
        all = [7, 8, 9]
        print("changing global:", all)
    
    def inner3():
        print("inner3 says:", all)
        
    inner1()
    print("checking 'all':", all)
    inner2()
    print("checking 'all':", all)
    inner3()
foo()
print("now global is", all)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
builtin: <built-in function all>
global: [1, 2, 3]
enclosed: [1, 2, 3, 'changed!']
checking 'all': [1, 2, 3, 'changed!']
changing global: [7, 8, 9]
checking 'all': [1, 2, 3, 'changed!']
inner3 says: [1, 2, 3, 'changed!']
now global is [7, 8, 9]
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 1
b = 3.1415926
c = "old string"

def f():
    print(a)
    global b

    b = 2
    c = "new string"

f()
print(a, b, c)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
1
1 2 old string
```
{% endcode %}



* `a` - free variable
* `b` - global variable
* `c` - local variable

In case above we don't have variable `a` in local scope so we go upper - and take it from global scope.

If the nearest enclosing scope for a free variable contains a global statement, the free variable is treated as a global.


🪄 _<mark style="color:green;">Code:</mark>_

```python
# Global variables
a = 0 
b = 30

def do_job( ): 
    a = 100    # Creating local variable which won't affect global one
    global b   # Marking absolute variable as global 
    b = 888    # Changing it will change global variable
    print("Inside the function -> a:", a)
    print("Inside the function -> b:", b)

do_job()

print("Outside the function -> a:", a)
print("Outside the function -> b:", b)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Inside the function -> a: 100
Inside the function -> b: 888
Outside the function -> a: 0
Outside the function -> b: 888
```
{% endcode %}



Get all locals, globals:
* ```locals()```
* ```globals()```

Note: in global scope locals and globals are the same.


🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 5
b = 10
def f():
    c = 25
    global b
    print(locals())
f()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
{'c': 25}
```
{% endcode %}



### Enclosed scope

Scope that is between global and local in nested functions


🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 'global variable'

def outer():
    a = 'enclosed variable'
    
    def inner():
        a = 'local value'
        print(a)
    
    inner()

outer()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
local value
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 'global variable'

def outer():
    a = 'enclosed variable'
    
    def inner():
        print(a)
    
    inner()

outer()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
enclosed variable
```
{% endcode %}



Introducing ```nonlocal``` statement which marking variable as enclosed (just like ```global``` does for global scope)


🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 'global variable'

def outer():
    a = 'enclosed variable'
    print(a)
    
    def inner():
        nonlocal a
        a = "changed enclosed variable"
        print(a)
    
    inner()
    print(a)
outer()
print(a)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
enclosed variable
changed enclosed variable
changed enclosed variable
global variable
```
{% endcode %}



Assign operation creates a local variable by default (if not `global` or `nonlocal` used for that variable).


🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 25
def foo():
    # global a
    a += 30  # a = a + 30
    
    b = a + 25
    return a, b
foo()
```


    

    UnboundLocalErrorTraceback (most recent call last)

    <ipython-input-3-591bdaeb3bef> in <module>
          6     b = a + 25
          7     return a, b
    ----> 8 foo()
    

    <ipython-input-3-591bdaeb3bef> in foo()
          2 def foo():
          3     # global a
    ----> 4     a += 30  # a = a + 30
          5 
          6     b = a + 25


    UnboundLocalError: local variable 'a' referenced before assignment



🪄 _<mark style="color:green;">Code:</mark>_

```python
a = 25
def foo(a=a):
    a += 30  # a = a + 30
    return a
foo()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
55
```
{% endcode %}




### Closures

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Functions can use variables from outer scopes.

Also it's worth to mention that those variables are searched only when function is called.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def foo():
    print(i)
    
i = 5
foo()
```

    5



🪄 _<mark style="color:green;">Code:</mark>_

```python
def foo():
    a = 5
    
    def inner():
        return a
    
    print("Running inner:", inner())
    
    return inner

#print(foo())
result = foo()
print(result)
print("Result of running inner function:", result())
```

    Running inner: 5
    <function foo.<locals>.inner at 0x7f3e881fe488>
    Result of running inner function: 5


How can `inner` know about `a` if `foo` is already returned and all we can't access to it's local variables normally?


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("Free vars:", result.__code__.co_freevars)
print(result.__closure__)
cell = result.__closure__[0]
print("Free var #1 value:", cell.cell_contents)
```

    Free vars: ('a',)
    (<cell at 0x7f3e88272258: int object at 0x5594948e94a0>,)
    Free var #1 value: 5