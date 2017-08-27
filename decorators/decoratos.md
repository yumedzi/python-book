# Decorators basics

> Decorator is design pattern. It dynamically alters the functionality of a function, method, or class without having to directly use subclasses or change the source code of the function being decorated.

> In Python decorators allow you to make simple modifications to callable objects like functions, methods, or classes.

* Idea is to alter function or method without a mess and confusion:

```python
def some_transformation(func):
    # doing something with func


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

> `Function(Function)` --> `Function`


`1`. Function is first-class object. Don't panic - it means that it is the same object as everything else. That's why we can assign function to another variable.


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

    LaLaLa
    LaLaLaLaLaLaLaLaLaLaLaLaLaLaLa
    Oops, Exception:  name 'song' is not defined
    <function Super Song at 0x103fe2a60>
    

`2`. We can define function everywhere! It will exist in that namespace only. #easy!


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

    New pop-hit: Tync-Tync-Boom-Oooh-Toonc-Beep-Beep-Boom-Beep-Toonc
    Notes: Si,La,Do,Fa,Re,La,Do,La,Re,Do
    

Of course we can't access internal functions in any way...


```python
try:
    _random_music(5)
except NameError as e:
    print("Oh, we can't acces this function outside:", e)
```

    Oh, we can't acces this function outside: name '_random_music' is not defined
    

`3`. We can even `return` function as function's result. After this we can use that object as new function itself.



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

    New pop-hit: Toonc-Oooh-Oooh-Tync-Oooh-Oooh-Toonc-Oooh-Toonc-Oooh-Tync-Toonc-Boom-Oooh-Beep
    Notes: Do,Fa,Si,Si,Do,Do,Do,Do,Fa,Do,La,Fa,Re,La,Si
    New pop-hit: Oooh-Toonc
    Notes: Si,Re
    

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


```python
def my_deco(func): 
    def wrapper(name="Jessy", *args, **kwargs): 
        name += " Walter"
        print(">>> Before running function")
        func(name, *args, **kwargs) 
        print(">>> After running function")
        
    return wrapper

@my_deco
def my_name(name="WW"):
    print("Remember my name:", name)

my_name("Walter")
```

Output:
```
>>> Before running function
Remember my name: Walter Walter
>>> After running function
```    

Another example:

Adding dollar sign to text


```python
def dollar(fn): 
    def wrapper(*args): 
        return '$' + str(fn(*args)) 
    return wrapper

@dollar
def price(amount, tax_rate): 
    return amount + amount*tax_rate
```

```
>>> print(price)
<function dollar.<locals>.wrapper at 0x1047a2b70>

>>> print(price(100,0.1))
$110.0
```
   

More, more examples!!!


```python
def count(f): 
    print("New deco init...")
    
    def inner(*args, **kwargs): 
        inner.counter += 1 
        return f(*args, **kwargs)
    
    inner.counter = 0 
    return inner

@count 
def my_func(): 
   pass

[my_func() for _ in range(13)]
print(my_func.counter)
my_func() # +1
print(my_func.__dict__)
```
Output:

    New deco init...
    13
    {'counter': 14}
    

Shown above decorator is call counter.

### Evolution of decorator

Let's create deco step by step!


```python
def my_deco(func):
    "Deco that simply returns original function"
    return func

@my_deco
def test1(x):
    return x

test1(25)
```

Output:

    25

``python
def my_deco(func):
    print("Init...") # We'll see this once
    return func

@my_deco
def test1(x):
    return x

print(test1(25))
print(test1(48))   
```

Output:

    Init...
    25
    48
    

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

Output:

    Init...
    25
    2017-06-02 11:42:54.937561
    

Tro-lo-lo decorator which return completely other function than original one:


```python
def bad_deco(func):
    return lambda *args, **kwargs: "HAhahahahha Trololo"

@bad_deco
def test1(x):
    return x

test1(45)
```

Output:

    'HAhahahahha Trololo'


One more example:

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
Output:

    <function my_deco.<locals>.wrapper at 0x10483a488>
    25
    

Adding some counter to wrapper to be able to see in test1:


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
print(test1.counter)
```

Output:

    25 48
    2
    

Final version:

```python
def my_deco(func): # FINAL VERSION OF IDEAL DECORATORS
    print("Init...")
    
    def wrapper(*args):
        wrapper.counter += 1
        print("Before running!...")
        res = func(*args)
        if res:
            print("Result is:", res)
        print("After running....")
 
    wrapper.created_at = "2234234876328764"
    wrapper.counter = 0

    return wrapper
```

You want more?... 

Ok. It is very useful timer decorator


```python
import time 

def timer(f): 
    def inner(*args, **kwargs): 
        t = time.time() 
        res = f(*args, **kwargs) 
        print('time spent: %.5s seconds' %(time.time() - t) )
        return res
    return inner

@timer 
def my_fnc(): 
    return "Length: " + str(len([pow(i,10) for i in range(4000000)]))

my_fnc()
```
Output:

    time spent: 2.880 seconds
    'Length: 4000000'
