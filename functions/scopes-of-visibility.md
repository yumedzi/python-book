# Scopes of visibility

> All variables in a program may not be accessible at all locations in that program. This depends on where you have declared a variable. 

> The scope of a variable determines the portion of the program where you can access a particular identifier. 

Scopes of visibility in Python:
* Builtin variables
* Global variables
* Enclosed variables
* Local variables

The search is goes only in those 4 places!

![](/assets/scope_resolution_1.png)


Local variables can be accessed only inside the function in which they are declared, whereas global variables can be accessed throughout the program body by all functions. When you call a function, the variables declared inside it are brought into scope. Use ```global```to access global variable.

If a name is bound in a block, it is a **local variable** of that block, unless declared as `nonlocal` or `global`. If a name is bound at the module level, it is a **global variable**. (The variables of the module code block are local and global.) If a variable is used in a code block but not defined there, it is a **free variable**.


```python
print("builtin:", all)
all = [1, 2, 3]
print("global:", all)
def foo():
    all = [4, 5, 6] 
    
    def inner1():
        nonlocal all
        all.append(7)
        print("enclosed:", all)
        
    def inner2():
        all = [7, 8, 9]
        print("local:", all)
        
    inner1()
    print(all)
    inner2()
    print(all)
foo()
```
Output:

    builtin: [1, 2, 3]
    global: [1, 2, 3]
    enclosed: [4, 5, 6, 7]
    [4, 5, 6, 7]
    local: [7, 8, 9]
    [4, 5, 6, 7]


One more example of three types of variables:
```python
a = 1
b = 3.1415
c = "old string"

def f():
    print (a)
    global b
    
    b = 2
    c = "new string"
f()
print(a, b, c)
```

    1
    1 2 old string


* `a` - free variable
* `b` - global variable
* `c` - local variable

In case above we don't have variable `a` in local scope so we go upper - and take it from global scope.

If the nearest enclosing scope for a free variable contains a global statement, the free variable is treated as a global.


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
Output:

    Inside the function -> a: 100
    Inside the function -> b: 888
    Outside the function -> a: 0
    Outside the function -> b: 888


Get all locals, globals:
* ```locals()```
* ```globals()```

Note: in global scope locals and globals are the same.


```python
a = 5
b = 10
def f():
    c = 25
    global b
    print(locals())
f()
```
Output:

    {'c': 25}


### Enclosed scope

Scope that is between global and local in nested functions


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
Output:

    local value

And example of enclosed variable:

```python
a = 'global variable'

def outer():
    a = 'enclosed variable'
    
    def inner():
        print(a)
    
    inner()

outer()

```
Output:

    enclosed variable


Introducing ```nonlocal``` statement which marking variable as enclosed (just like ```global``` does for global scope)


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
Output:

    enclosed variable
    changed enclosed variable
    changed enclosed variable
    global variable


Assign operation creates a local variable by default (if not `global` or `nonlocal` used for that variable).


```python
a = 25
def foo():
    a += 30
foo()
```


    ---------------------------------------------------------------------------

    UnboundLocalError                         Traceback (most recent call last)

    <ipython-input-3-c1ac3a635076> in <module>()
          2 def foo():
          3     a += 30
    ----> 4 foo()
    

    <ipython-input-3-c1ac3a635076> in foo()
          1 a = 25
          2 def foo():
    ----> 3     a += 30
          4 foo()


    UnboundLocalError: local variable 'a' referenced before assignment


### Closures *

Functions can use variables from outer scopes.

Also it's worth to mention that those variables are searched only when function is called.


```python
def foo():
    print(i)
    
i = 5
foo()
```
Output:

    5



```python
def foo():
    a = 5
    
    def inner():
        return a
    
    print("Running inner:", inner())
    
    return inner
#print(foo())
result = foo()
result
print("Result of running inner function:", result())
```
Output:

    Running inner: 5
    Result of running inner function: 5


How can `inner` know about `a` if `foo` is already returned and all we can't access to it's local variables normally?


```python
print("Free vars:", result.__code__.co_freevars)
print(result.__closure__)
cell = result.__closure__[0]
print("Free var #1 value:", cell.cell_contents)

```
Output:

    Free vars: ('a',)
    (<cell at 0x104791258: int object at 0x100288a00>,)
    Free var #1 value: 5

