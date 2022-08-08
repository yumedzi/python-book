# Decorators

> Decorator is design pattern. It dynamically alters the functionality of a function, method, or class without having to directly use subclasses or change the source code of the function being decorated.

> In Python decorators allow you to make simple modifications to callable objects like functions, methods, or classes.

* Idea is to alter function or method without a mess and confusion:

```python
def some_transformation(func):
    # doing something with func
    return func2


def foo(*args):
    # doing something...
foo = some_transformation(foo)
```

* Decorator will make this look really more readable and nice:
```python
@some_transformation
def foo(*args):
    # doing something...
```

## Motivation section

Examples from real world

### Django

To avoid checking routine things like cookie, check for it's existense in DB and redirecting to login page if user is not logged in. 

Another decorator checks if the user has needed rights to see this page. 

```python
@login_required
@staff_required
def view_project_adm(request, client_id):
    request.session['adm_client_view'] = True
    project = get_object_or_404(Project, pk=id)
    return render('view_project.html', project=project)
```


### Flask

Decorator binds the function to specific route

```python
@app.route("/project/<id>")
def view_projects(id):
    project = Project.query.filter(Project.pk == id).first()
    return render_template('view_projects.html', project=project)
```




## Some reminder about functions

> In a nutshell decorator is a function that take another (decorated) function as argument and returns transformed function. So it is:

> `Function(Function)` &xrarr; `Function`


`1`. Function is first-class object. Don't panic - it means that it is the same object as everything else. That's why we can assign function to another variable.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def song(times=3): 
    return "La" * times

print(song())

scream = song # song is boring! let's call it scream
print(scream(15))
del song # delete old variable
try:
    song()
except NameError as e:
    print("Oops, Exception: ", e)
scream.__qualname__ = "Super Song"
print(scream)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
LaLaLa
LaLaLaLaLaLaLaLaLaLaLaLaLaLaLa
Oops, Exception:  name 'song' is not defined
<function Super Song at 0x103fe2a60>
```
{% endcode %}
`2`. We can define function everywhere! It will exist in that namespace only. #easy!


🪄 _<mark style="color:green;">Code:</mark>_

```python
def music(beats=3): 
    import random
    
    def _random_music(times): 
        notes = "La", "Do", "Re", "Fa", "Si"
        return ",".join(random.choice(notes) for i in range(times))
    
    def _random_effects(times):
        effects = "Toonc", "Tync", "Boom", "Beep", "Oooh"
        return "-".join(random.choice(effects) for i in range(times))

    return "New pop-hit: {}\nNotes: {}".format(_random_effects(beats), _random_music(beats))

print(music(10))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
New pop-hit: Tync-Tync-Boom-Oooh-Toonc-Beep-Beep-Boom-Beep-Toonc
Notes: Si,La,Do,Fa,Re,La,Do,La,Re,Do
```
{% endcode %}
Of course we can't access internal functions in any way...


🪄 _<mark style="color:green;">Code:</mark>_

```python
try:
    _random_music(5)
except NameError as e:
    print("Oh, we can't acces this function outside:", e)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Oh, we can't acces this function outside: name '_random_music' is not defined
```
{% endcode %}
`3`. We can even `return` function as function's result. After this we can use that object as new function itself.



🪄 _<mark style="color:green;">Code:</mark>_

```python
def party(kind=""):
    def fun_party():
        return music(15)

    def sad_party():
        return music(2)
    
    if "fun" in kind:
        return fun_party
    else:
        return sad_party

some_party = party(kind="veryfun")
print( some_party() )
print(party()())
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
New pop-hit: Toonc-Oooh-Oooh-Tync-Oooh-Oooh-Toonc-Oooh-Toonc-Oooh-Tync-Toonc-Boom-Oooh-Beep
Notes: Do,Fa,Si,Si,Do,Do,Do,Do,Fa,Do,La,Fa,Re,La,Si
New pop-hit: Oooh-Toonc
Notes: Si,Re
```
{% endcode %}
## Decorator syntax and examples

> Idea – function which returns processed result of another function 

General format of usage:

```python
@mydecorator
def myfunc():
    pass
```
It is the **absolutely** the same as:

```python
def myfunc():
    pass
myfunc = mydecorator(myfunc)

```

where `mydecorator` is some function...

Example of decorator realization


🪄 _<mark style="color:green;">Code:</mark>_

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def my_deco(func): 
    def wrapper(): 
        print(">>> Before running function")
        print(func()) 
        print(">>> After running function")
        
    return wrapper

@my_deco
def greet():
    return f"Hello!"

greet()
```


📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
>>> Before running function
Hello!
>>> After running function
```
{% endcode %}
Another example:

Adding dollar sign to text


🪄 _<mark style="color:green;">Code:</mark>_

```python
def dollar(fn): 
    def wrapper(*args, **kwargs): 
        print(f"Args are: {args}, KWArgs: {kwargs}")
        return '$' + str(fn(*args, **kwargs)) 
    return wrapper

@dollar
def price(amount, tax_rate): 
    return amount + amount*tax_rate   

print(price)

print(price(100, tax_rate=.1))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
<function dollar.<locals>.wrapper at 0x7f208019f8b0>
Args are: (100,), KWArgs: {'tax_rate': 0.1}
$110.0
```
{% endcode %}
The same example, but in one line:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def dollar(func): 
    return lambda *args, **kwargs: f"${func(*args, **kwargs)}"

@dollar
def f():
    return 100

f()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'$100'
```
{% endcode %}
More, more examples!!!


🪄 _<mark style="color:green;">Code:</mark>_

```python
def json(func):                              
    def wrapper(*args, **kwargs):            
        import json                          
        result = func(*args, **kwargs)       
        return json.dumps({"result": result})
                                             
    return wrapper                           
                                        
                                             
@json                                       
def f(x, y):                                 
    return x ** y                            
                                             
                                             
f(3, 5)                                      
'{"result": 243}'
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'{"result": 243}'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
def count(f): 
    print("New deco init...")
    
    def inner(*args, **kwargs):
        #inner.counter = getattr(inner, "counter", 0) + 1 
        inner.counter += 1
        return f(*args, **kwargs)
    
    inner.counter = 0
    return inner

@count 
def my_func(): 
   pass

print(my_func.counter)
[my_func() for _ in range(9)]
my_func() # +1
print(f"my_func.counter = {my_func.counter}")
print(f"my_func.__dict__ = {my_func.__dict__}")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
New deco init...
0
my_func.counter = 10
my_func.__dict__ = {'counter': 10}
```
{% endcode %}
Shown above decorator is call counter.

### Evolution of decorator

Let's create deco step by step!


🪄 _<mark style="color:green;">Code:</mark>_

```python
def my_deco(func):
    "Deco that simply returns original function"
    return func

@my_deco
def test1(x):
    return x

test1, test1(100500)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(<function __main__.test1(x)>, 100500)
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
def my_deco(func):
    print("Init...") # We'll see this once
    return func 

@my_deco
def test1(x):
    return x

print(test1(25))
print(test1(48))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Init...
25
48
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
def capture_time(func):
    import datetime
    
    print("Init...")
    func.created_at = str(datetime.datetime.now())
    return func

@capture_time
def test1(x):
    return x

print(test1(25))
print(test1.created_at)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Init...
25
2019-12-09 10:17:56.486420
```
{% endcode %}
Tro-lo-lo decorator which return completely other function than original one:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def bad_deco(func):
    return lambda *args, **kwargs: "HAhahahahha Trololo"

@bad_deco
def test1(x):
    return x ** 100000000000000000

# def test1(x)
#     return x
# test1 = bad_deco(test1)

test1()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'HAhahahahha Trololo'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
def my_deco(func):
    "Again doing nothing!"
    def wrapper(*args):
        return func(*args)
 
    return wrapper

@my_deco
def test1(x):
    return x
    
print(test1)
print(test1(25))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
<function my_deco.<locals>.wrapper at 0x10483a488>
25
```
{% endcode %}
Adding some counter to wrapper to be able to see in test1:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def my_deco(func):
    "Again doing nothing!"
    def wrapper(*args):
        wrapper.counter += 1
        return func(*args)
 
    wrapper.counter = 0
    return wrapper
    
@my_deco
def test1(x):
    return x

print(test1(25), test1(48))
print(test1(1))
print(test1.counter)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
25 48
1
3
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
def my_deco(func): # FINAL VERSION OF IDEAL DECORATOR
    print("Init of decorator...")
    import datetime
    
    def wrapper(*args, **kwargs):
        wrapper.counter += 1
        wrapper.last_run = str(datetime.datetime.now())
        print(">>> Before running!...")
        res = func(*args, **kwargs)
        if res:
            print(">>> Result is:", res)
        print(">>> After running....")
        return res
 
    wrapper.created_at = str(datetime.datetime.now())
    wrapper.counter = 0
    
    wrapper.info = lambda: f'This function was decorated by IDEAL DECORATOR on {wrapper.created_at}' +\
        f' and ran {wrapper.counter} time{"s" if wrapper.counter != 1 else ""} (last run: {wrapper.last_run})'
    return wrapper

@my_deco
def foo(x, y):
    return x ** y

foo(10, 40)
foo(10, 40)

foo.info()
```


📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Init of decorator...
>>> Before running!...
>>> Result is: 10000000000000000000000000000000000000000
>>> After running....
>>> Before running!...
>>> Result is: 10000000000000000000000000000000000000000
>>> After running....





'This function was decorated by IDEAL DECORATOR on 2020-12-30 07:52:06.535243 and ran 2 times (last run: 2020-12-30 07:52:06.536808)'
```
{% endcode %}
You want more?... 

Ok. It is very useful timer decorator


🪄 _<mark style="color:green;">Code:</mark>_

```python
def timer(f): 
    import time 
    
    def inner(*args, **kwargs): 
        start_time = time.time() 
        res = f(*args, **kwargs) 
        print(f'Function: {f.__name__}({(", ".join(map(str, args)) + ", ") if args else ""}{kwargs}), time spent: %.5s seconds' %(time.time() - start_time) )
        return res
    return inner

@timer 
def my_fnc(x=1): 
    return "Length: " + str(len([pow(i,10) for i in range(4000000)]))

@timer
def f():
    a = [str(x)*10 for x in range(10000000)]

l = my_fnc(1)
l2 = f()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Function: my_fnc(1, {}), time spent: 3.666 seconds
Function: f({}), time spent: 7.063 seconds
```
{% endcode %}
"Fakely long runnning" decorator


🪄 _<mark style="color:green;">Code:</mark>_

```python
def work(func):
    def wrapper(*args, **kwargs):
        import time
        for _ in range(3):
            print("Work is in progress....")
            time.sleep(1)
        return func(*args, **kwargs)
    return wrapper

@work
def f():
    print("Done")
    
f()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Work is in progress....
Work is in progress....
Work is in progress....
Done
```
{% endcode %}
It is possible to add some random strings to show during "fake running" time window:


🪄 _<mark style="color:green;">Code:</mark>_

```python
def work(func):
    phrases = [
        "Work in progress....",
        "Calculating shifts in raw data abstract vectors",
        "Alligning matrixes of indexes for data frames",
        "Reformatting data sources", "Traversing trough raw data internals",
        "Validating obtained subprocess results"
    ]

    def wrapper(*args, **kwargs):
        import time
        import random

        for _ in range(3):
            print(random.choice(phrases) + "...")
            time.sleep(1)
        return func(*args, **kwargs)
    return wrapper

@work
def calc_sum(x, y):
    return x + y

calc_sum(2, 2)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Traversing trough raw data internals...
Validating obtained subprocess results...
Alligning matrixes of indexes for data frames...





4
```
{% endcode %}
Super cool decorator that controls the time of execution for decorated function and stops it in case of exceeding that time:


```python
def time_limit(func):
    "Giving <func> 3 seconds to run"
    import signal

    def signal_handler(signum, frame):
        raise TimeoutError

    def wrapper(*args, **kwargs):
        signal.signal(signal.SIGALRM, signal_handler)
        signal.alarm(3)  # <--- hardcoded Num of seconds
        try:
            return func(*args, **kwargs)
        except TimeoutError:
            print("Timed out! ")

    return wrapper
```

Let's check how it works:


🪄 _<mark style="color:green;">Code:</mark>_

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;"></mark><mark style="color:green;">📟</mark> <mark style="color:green;"></mark>_<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
import time

@time_limit
def long(seconds):
    time.sleep(seconds)
    return "Done"

print(">>> Running quick / 1 second:")
print(long(1))

print(">>> Running long / 4 seconds:")
print(long(4))
```


📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
>>> Running quick / 1 second:
Done
>>> Running long / 4 seconds:
Timed out! 
None
```
{% endcode %}
## Chaining decorators

It is possible to chain and use multiple decorators in succession.


```python
def makebold(fn): 
    def wrapped(*args, **kwargs): 
        return "<b>" + str(fn(*args, **kwargs)) + "</b>" 
    return wrapped

def makeitalic(fn): 
    def wrapped(*args, **kwargs): 
        return "<i>" + str(fn(*args, **kwargs)) + "</i>" 
    return wrapped

def makered(fn): 
    def wrapped(*args, **kwargs): 
        return "<span style='color: red;'>" + str(fn(*args, **kwargs)) + "</span>"
    return wrapped
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
@makebold
@makeitalic
@makered
def hello(text="Goodbye World!"):
    return text

# hello = makebold(makeitalic(makered(hello)))

hello()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
"<b><i><span style='color: red;'>Goodbye World!</span></i></b>"
```
{% endcode %}
<b><i><span style='color: red;'>Goodbye World!</span></i></b>


🪄 _<mark style="color:green;">Code:</mark>_

```python
@makebold
@makeitalic   
@makebold 
@makebold
def hello(text="Goodbye again, World!"):
      return text

hello()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'<b><i><b><b>Goodbye again, World!</b></b></i></b>'
```
{% endcode %}
As resume memoization rule:
    
> Decorator is 

> * `function`
>     * that takes `function` as argument and returns
>        * `function`
            * <span style='color: gray;'>which substitute given function</span>

To check your understanding of decorator to this point - try to explain what the following decorator does.

* What the purpose of riddle_deco?
* Is there any issues in riddle_deco?

Hints:
* remember counter decorator!


```python
def riddle_deco(f):
    def _f(bill, *args):
        if not hasattr(_f, "_val"):
            _f._val = dict()
        
        if not bill in _f._val:
            _f._val[bill] = f(bill, *args)
        return _f._val[bill]

    return _f

@riddle_deco
def calc_tips(bill, tip_rate=0.10):
    return int(bill * tip_rate)
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
calc_tips(100)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
10
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
calc_tips(200, 0.05)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
10
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
print(calc_tips(100, 0.05)) # Surprise! Why?
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
10
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
print(calc_tips._val)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
{100: 10, 200: 10}
```
{% endcode %}
Way to improve this cashing decorator - change key to a tuple that contains a `tip_rate` also. In this way we'll cover all possible cases.


```python
def riddle_deco(f):
    def _f(bill, tip_rate=0.10, *args):
        if not hasattr(_f, "_val"):
            _f._val = dict()
        
        if not (bill, tip_rate) in _f._val:
            _f._val[bill, tip_rate] = f(bill, tip_rate, *args)
        return _f._val[bill, tip_rate]

    return _f

@riddle_deco
def calc_tips(bill, tip_rate=0.10):
    return int(bill * tip_rate)
```

And one-liner!


```python
def riddle_deco(f):
    return lambda b,r=0.10: f.__dict__.setdefault("_val", {}).setdefault((b, r), f(b, r))
```

## Some internals

### Preserving attributes

Decorated function loosing it's name and docstring. In fact we are substituting one function with completely different one that just uses the first one.


🪄 _<mark style="color:green;">Code:</mark>_

```python
calc_tips

print("Function name:", calc_tips.__name__)
print("Function docstring:", calc_tips.__doc__)
print(calc_tips)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Function name: _f
Function docstring: None
<function riddle_deco.<locals>._f at 0x7fd4f15baea0>
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
# "Fixing":
calc_tips.__name__       = "test"
calc_tips.__qualname__   = "test"

print("Function name:", calc_tips.__name__)
print(calc_tips)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Function name: test
<function test at 0x7fd4f15baea0>
```
{% endcode %}
We can do this in decorator to fix all these issues


🪄 _<mark style="color:green;">Code:</mark>_

```python
def deco(f):
    def ugly_wrapper_name(*args, **kwargs):
        return f(*args, **kwargs)
    ugly_wrapper_name.__name__ = f.__name__
    ugly_wrapper_name.__doc__ = f.__doc__
    ugly_wrapper_name.__qualname__ = f.__qualname__
    return ugly_wrapper_name

@deco
def pretty_func(x="Mew mew mew"):
    "Print something nice"
    print(x)
    
pretty_func()
print(pretty_func.__name__)
print(pretty_func.__doc__)
print(pretty_func)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Mew mew mew
pretty_func
Print something nice
<function pretty_func at 0x7f210c6936a8>
```
{% endcode %}
Alternative - suggested method - to use `functools.wraps` decorator which will automatically assign wrapper function’s `__module__`, `__name__`, `__qualname__`, `__annotations__` and `__doc__`. 


🪄 _<mark style="color:green;">Code:</mark>_

```python
from functools import wraps

def my_decorator(f):
    @wraps(f)
    def wrapper(*args, **kwds):
        print('Calling decorated function')
        return f(*args, **kwds)
    return wrapper

@my_decorator
def example():
    """Docstring"""
    print('Called example function')

example()

print(example.__name__)
print(example.__doc__)
print(example)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Calling decorated function
Called example function
example
Docstring
<function example at 0x104ad2ea0>
```
{% endcode %}
### One-time decorator

Haiku about subject:

> Life is beatiful

> and cruel at the very same time

> for decorator-one-timer


🪄 _<mark style="color:green;">Code:</mark>_

```python
def batterfly(f):
    print("It was nice, thank you for all..")
    return f

@batterfly
def func():   # func = batterfly(func)
    print("Some text") 
    
func()
func()

@batterfly
def f():
    1/0
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
It was nice, thank you for all..
Some text
Some text
It was nice, thank you for all..
```
{% endcode %}
