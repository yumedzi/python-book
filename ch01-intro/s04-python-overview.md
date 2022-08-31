# Python overview
<br>
To get you grasp of an idea about Python it's better to just fly over it awhole. To see main syntax nuances, basic operations and workflow. We won't stop to explain everything in detail as it will be covered in next sessions. Now it's just a show-off.

So, in next few slides we are going to see:
* Basic types
* Basic operators and methods
* Conditions
* Functions
* OOP
* Exceptions

## Basic types

<span title="This is important" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">ℹ️</span>

| Type        | Name         | Short description                        | Mutable | Example            |
|-------------|--------------|------------------------------------------|---------|---------------------------
| `NoneType`  | None         | "Empty" value                            | No    |  `None`               |
| `bool`      | Boolean      | Boolean value  (`True` or `False`)       | No    |  `True`               | 
| `int`       | Integer      | Integer numbers                          | No    |  `42`                 |
| `float`     | Float        | Floating point number                    | No    |  `23.43`              |
| `str`       | String       | Textual data - sequense of characters    | No    |  `"Hello!"`           |
| `list`      | List         | Mutable sequense of any kind of objects  | Yes   |  `[1, 2, 3]`          |
| `tuple`     | Tuple        | Immutable sequense of objects            | No    |  `(1, 2, 3)`          |
| `set`       | Set          | Mutable collection of unique objects     | Yes   |  `{1, 2, 3}`          |
| `frozentset`| Frozen Set   | Immutable collection of unique objects   | No    |  `frozenset({1, 2, 3})`          |
| `dict`      | Dictionary   | The collection of key-value pairs        | Yes   |  `{"name": "Johnny", "second_name": "Walker" }`  |
|   

### Immutable types (cannot be changed after creation)
* str
```python
some_str = "I'm a string!" 
```
* int
```python
some_int = 14
```
* float
```python
some_float = 23.23 
```
* tuple
```python
some_tuple = (13, 45, "Yo!", 34.3) 
```

### Mutable types (can be changed)
* list
```python
some_list = [14, "string", 14, [1, 2]] 
```
* set
```python
some_set = {(1, 2), 'string', 14}
```
* dict
```python
some_dict = {"name":"John", "sname":"Smith"}
```

### Basic operators:
* Assignment operators: 
    * `=`, `+=`, `*=`, `-=`, `/=`
* Comparison operators: 
    * `==`, `!=`, `>`, `<`, `<=`, `>=` 
    * `is`
* Logical operators: 
    * `and`, `or`, `not`
* Arithmetic operators: 
```python
number = 1 + 2 * 3 / 4.0 
another_num = 11 % 3 ** 3 // 2
```

### Basic operators, sequences:

* String operators: 
```python
test_string = "Hello" + " " + "World!" 
crazy_string = "Yo!" * 10 
print(test_string[3])
len(test_string) 
```
* List operators: 
```python
one_list = ["Ring of elves", "Ring of dwarves"] 
all_rings = one_list + ["Ring of men"] 
len(all_rings)
all_rings.append("Ring of Power") # Also: extend(), count(), reverse(), sort()
```

### Conditions, cycles

* Conditions

```python
if a > b: 
    print("a is greater than b")
elif a > 0:
    print("But it is still > 0")
else:
    print("Something is wrong...")
```

* Cycles

```python
for i in range(1, 10): 
    print(i)

while True: 
    print("Kill process or Ctrl-C :(")
```

### Importing

```python
import math
from math import cos
from random import choice as ch
from math import *

math.cos(180)
cos(49)
ch([1, 2, 4])
pi
```


### Work with Files

```python
f = open("text.txt") 
line = f.readline() 
while line: 
    print(line, end="") # suppress \n after each line as the line already has it
    line = f.readline() 
f.close()
```

```python
# More easy way:
with open("/tmp/file.txt", "r", encoding="win1251") as f:
    print(f.readlines(), end="")
```


### Functions

Operator "def" is used for creating functions


🪄 _<mark style="color:red;">Code</mark>_:

```python
x = 10
def mult(a, b=5):
    return a * b + x

print(mult(4, 3))
print(mult(4))
print(mult(b=15, a=5))
print(mult(10))
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
22
30
85
60
```
{% endcode %}
Lambda function - short (functional) method of defining a function. Used for sorting, building jump tables, when the function is not planned to be used after some operation and with `map`/`filter`.


🪄 _<mark style="color:red;">Code</mark>_:

```python
mult2 = lambda x, y: x * y
mult2(5, 6)
```




📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
30
```
{% endcode %}
🪄 _<mark style="color:red;">Code</mark>_:

```python
functions = [lambda x: x+100, lambda x: x-100] # Jump table
print(functions[0](50), functions[1](50), sep="; ")
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
150; -50
```
{% endcode %}
### Misc.

#### Swapping two variables


🪄 _<mark style="color:red;">Code</mark>_:

```python
a, b = 45, "54"
a, b = b, a

a, b
```




📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
('54', 45)
```
{% endcode %}
#### Read keyboard input

```python
print(input("Please enter something")) # Python 3
print(raw_input("Please enter something")) # Python 2
```


### Passing argument to function

There is a common question - how exactly arguments are passing in Python's functions. Usually there are two cases: value and pointer. By here we don't have either of those - because everything in python is wrapped in Python objects.

So, argument passing to a function is done not by value (we don't have "raw" data in Python, only objects that wrapping it) and not by reference (reference is int number of memory location). This is done by object-reference. In other words we are passing object itself (it's almost like passing the pointer to an object in memory).


🪄 _<mark style="color:red;">Code</mark>_:

```python
def testme(my_list): 
    my_list.append("END")
    print(my_list)
my_list = [1]
testme(my_list)
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
[1, 'END']
```
{% endcode %}
### Decorators


🪄 _<mark style="color:red;">Code</mark>_:

```python
def deco(f): 
    def w(*args, **kwargs): 
        print("*** Showing results :) ***")
        return f(*args, **kwargs) 
    return w

@deco
def show_something(): 
    print("Main function output")
    
show_something()
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
*** Showing results :) ***
Main function output
```
{% endcode %}
### OOP


In Python, everything is an object, even classes. Classes are object too! More of that, classes as objects have their own classes which called metaclasses. Multiple inheritance and mixins are supported.

The language supports extensive introspection of types and classes. Types can be read and compared—types are instances of type. The attributes of an object can be extracted as a dictionary.

Operators can be overloaded in Python by defining special member functions—for instance, defining __add__ on a class permits one to use the + operator on members of that class.



🪄 _<mark style="color:red;">Code</mark>_:

```python
class Foo:
    attr1 = "Some value"
    attr2 = "Boo!"
    
    def __str__(self):
        return "Nice warm object :)"
    
    def foo(self):
        return self.attr1
    
    def __init__(self, val=None): 
        print(f"Initializing new object with val={val}")
        if val is not None:
            self.attr1 = val

obj = Foo("Super Value")
print(obj)
print("Result of obj.foo():", obj.foo())
print(obj.attr1) 
print(obj.attr2)
print(Foo.attr1)
print(obj.foo())
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
Initializing new object with val=Super Value
Nice warm object :)
Result of obj.foo(): Super Value
Super Value
Boo!
Some value
Super Value
```
{% endcode %}
### Exceptions

Sometime Python encounters the error during the work of some code or function - it creates an event called exception. If this exception is not handled (the program doesn't expect it) Python stops stops the program execution.

For example the file with the following code will print the message about Traceback and never the line "You won't see me!":


🪄 _<mark style="color:red;">Code</mark>_:

```python
1/0
print("You won't see me!")
```


📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
---------------------------------------------------------------------------

ZeroDivisionError                         Traceback (most recent call last)

Input In [25], in <cell line: 1>()
----> 1 1/0
      2 print("You won't see me!")


ZeroDivisionError: division by zero
```
{% endcode %}
But we can handle this error, doing so tells Python that the occurrence of this error is expected and we don't need to stop the program.

Handling exceptions is done via `try`/`except`/`finally` blocks:


🪄 _<mark style="color:red;">Code</mark>_:

```python
try:
    1/0
except ZeroDivisionError:
    print("Oh, you tried to divide by 0! Nice try!")
else:
    print("You will see this when the error won't be encountered.")
finally:
    print("You will see this in any case - was error encountered or not.")
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
Oh, you tried to divide by 0! Nice try!
You will see this in any case - was error encountered or not.
```
{% endcode %}
