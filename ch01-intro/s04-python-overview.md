# Python overview
<br>
To get you grasp of an idea about Python it's better to just fly over it awhole. To see main syntax nuances, basic operations and workflow. We won't stop to explain everything in detail as it will be covered in next sessions. Now it's just a show-off.

So, in next few slides we are going to see:
* basic types
    * immutable
    * mutable
* basic operators and methods
* conditions
* OOP
* Exceptions

### Immutable types (cannot be changed after creation)
* str
🪄 _<mark style="color:green;">Code:</mark>_

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
🪄 _<mark style="color:green;">Code:</mark>_

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
🪄 _<mark style="color:green;">Code:</mark>_

```python
number = 1 + 2 * 3 / 4.0 
another_num = 11 % 3 ** 3 // 2
```

### Basic operators, sequences:

* String operators: 
🪄 _<mark style="color:green;">Code:</mark>_

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

🪄 _<mark style="color:green;">Code:</mark>_

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

🪄 _<mark style="color:green;">Code:</mark>_

```python
f = open("text.txt") 
line = f.readline() 
while line: 
    print(line, end="") # suppress \n after each line as the line already has it
    line = f.readline() 
f.close()
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
# More easy way:
with open("/tmp/file.txt", "r", encoding="win1251") as f:
    print(f.readlines(), end="")
```


### Functions

Operator "def" is used for creating functions


```python
x = 10
def mult(a, b=5):
    return a * b + x

print(mult(4, 3))
print(mult(4))
print(mult(b=15, a=5))
print(mult(10))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
22
30
85
60
{% endcode %}



### Misc.

#### Swapping two variables


```python
a, b = 45, "54"
a, b = b, a

a, b
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
('54', 45)
{% endcode %}




#### Read keyboard input

🪄 _<mark style="color:green;">Code:</mark>_

```python
print(input("Please enter something")) # Python 3
print(raw_input("Please enter something")) # Python 2
```


### Passing argument to function

There is a common question - how exactly arguments are passing in Python's functions. Usually there are two cases: value and pointer. By here we don't have either of those - because everything in python is wrapped in Python objects.

So, argument passing to a function is done not by value (we don't have "raw" data in Python, only objects that wrapping it) and not by reference (reference is int number of memory location). This is done by object-reference. In other words we are passing object itself (it's almost like passing the pointer to an object in memory).


```python
def testme(my_list): 
    my_list.append("END")
    print(my_list)
my_list = [1]
testme(my_list)
```

### Decorators


```python
def deco(f): 
    def w(*args, **kwargs): 
        print(">>> Showing results :)")
        return f(*args, **kwargs) 
    return w

@deco
def show_something(): 
    print("Main function output")
    
show_something()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
>>> Showing results :)
Main function output
{% endcode %}



### OOP


In Python, everything is an object, even classes. Classes are object too! More of that, classes as objects have their own classes which called metaclasses. Multiple inheritance and mixins are supported.

The language supports extensive introspection of types and classes. Types can be read and compared—types are instances of type. The attributes of an object can be extracted as a dictionary.

Operators can be overloaded in Python by defining special member functions—for instance, defining __add__ on a class permits one to use the + operator on members of that class.



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

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}```
Initializing new object with val=Super Value
Nice warm object :)
Result of obj.foo(): Super Value
Super Value
Boo!
Some value
{% endcode %}

    Super Value