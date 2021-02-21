# Python overview {#Python-overview}

To get you grasp of an idea about Python it's better to just fly over it awhole. To see main syntax nuances, basic operations and workflow. We won't stop to explain everything in detail as it will be covered in next sessions. Now it's just a show-off.

So, in next few slides we are going to see:

* basic types
  * immutable
  * mutable
* basic operators and methods
* conditions
* OOP
* Exceptions

### Immutable types \(cannot be changed after creation\) {#Immutable-types-(cannot-be-changed-after-creation)}

* str
  ```py
  some_str = "I’m a string!"
  ```
* int
  ```py
  some_int = 14
  ```
* float
  ```py
  some_float = 23.23
  ```
* tuple
  ```py
  some_tuple = (13, 45, "Yo!", 34.3)
  ```

### Mutable types \(can be changed\) {#Mutable-types-(can-be-changed)}

* list
  ```py
  some_list = [14, "string", 14, [1, 2]]
  ```
* set
  ```py
  some_set = {(1, 2), 'string', 14}
  ```
* dict
  ```py
  some_dict = {"name":"John", "second_name":"Smith"}
  ```

### Basic operators: {#Basic-operators:}

* Assignment operators:
  * `=`,`+=`,`*=`,`-=`,`/=`
* Comparison operators:
  * `==`,`!=`,`>`,`<`,`<=`,`>=`
* Logical operators:
  * `and`,`or`,`not`
* Arithmetic operators:
  ```py
  number = 1 + 2 * 3 / 4.0 
  another_num = 11 % 3 ** 3 // 2
  ```

### Basic operators, sequences: {#Basic-operators,-sequences:}

* String operators:

```py
test_string = "Hello" + " " + "World!" 
crazy_string = "Yo!" * 10 
print(test_string[3])
len(test_string)
```

* List operators:

```py
one_list = ["Ring of elves", "Ring of dwarves"] 
all_rings = one_list + ["Ring of men"] 
len(all_rings)
all_rings.append("Ring of Power") # Also: extend(), count(), reverse(), sort()
```

### Conditions, cycles {#Conditions,-cycles}

* Conditions:

```py
if a > b: 
      print("a is greater than b")
```

* Cycles:

```py
for i in range(1, 10): 
    print(i)

while True: 
    print("Kill process or Ctrl-C :(")
```

### Importing {#Importing}

```py
import math
from math import cos
from random import choice

math.cos(180)
cos(49)
choice([1, 2, 4])
```

### Work with Files {#Work-with-Files}

```py
f = open("text.txt") 
line = f.readline() 
while line: 
    print(line, end="") # supress \n after each line as the line already has it
    line = f.readline() 
f.close()
```

### Functions {#Functions}

Operator "def" is used for creating functions:

```py
def mult(a, b=5): 
    return a * b
```

```py
>>> mult(4, 10)
40
```

### Misc. {#Misc.}

#### Swapping two variables: {#Swapping-two-variables}

```py
>>> a, b = 45, 54
>>> a, b = b, a
>>> print(a, b)
54 45
```

#### Read keyboard input {#Read-keyboard-input}

```py
print(input("Please enter something")) # Python 3
print(raw_input("Please enter something")) # Python 2
```

### Passing argument to function {#Passing-argument-to-function}

There is a common question - how exactly arguments are passing in Python's functions. Usually there are two cases: value and pointer. By here we don't have either of those - because everything in python is wrapped in Python objects.

So, argument passing to a function is done not by value \(we don't have "raw" data in Python, only objects that wrapping it\) and not by reference \(reference is int number of memory location\). This is done by object-reference. In other words we are passing object itself \(it's almost like passing the pointer to an object in memory\).

```py
def testme(my_list): 
    my_list.append("END")
    print(my_list)
my_list = [1]
```

```py
>>> testme(my_list)
[1, 'END']
```

### Decorators {#Decorators}

```py
def deco(f): 
    def w(*args, **kwargs): 
        print(">>> Showing results:")
        return f(*args, **kwargs) 
    return w

@deco
def show_something(): 
    print("Main function ouput")
```

```py
>>> show_something()
 Showing results:
Main function ouput
```

### OOP {#OOP}

In Python, everything is an object, even classes. Classes are object too! More of that, classes as objects have their own classes which called metaclasses. Multiple inheritance and mixins are supported.

The language supports extensive introspection of types and classes. Types can be read and compared—types are instances of type. The attributes of an object can be extracted as a dictionary.

Operators can be overloaded in Python by defining special member functions—for instance, defining **\_\_add\_\_**  on a class permits one to use the **+** operator on members of that class.

```py
class Foo(object): 
    attr1 = "Some value"
    attr2 = "Boo!"

    def __str__(self):
        return "Nice warm object :)"

    def foo(self):
        return self.attr1

    def __init__(self, val=None): 
        print("Initializing new object!")
        if not val is None:
            self.attr1 = val
```

```py
>>> obj = Foo("Spam")
Initializing new object!

>>> print(obj)
Nice warm object :)

>>> print(obj.foo())
Spam

>>> print(obj.attr1) 
Spam

>>> print(obj.attr2)
Boo!
```



