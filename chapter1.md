# 1. "Hello World"

> This first session is an introduction to Python. It is "Bird's eye view" for this course.

#### Plan:

* [What is Python?](#What-is-Python?)
* [Python interpreter](#Python-interpreter)
* [Python Syntax](#Basic-syntax)
* [Basic types, operators](#Python-overview)
* [Installation, IDEs, etc.](#Installation,-IDEs-etc.)
* [Sources for self-learning](#Sources-for-self-learning)

### Canonical example {#Canonical-example}

```
print("Hello World!!")
```

```
Hello World!!
```

For Python 2:

```
>>> print "Hello World"
```

```
Hello World
```

## What is Python? {#What-is-Python?}

![](assets/import.png)

```
import antigravity
```

> Python is high-level dynamically typed interpreted programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than would be possible in languages such as C++ or Java.
>
> _There should be one — and preferably only one — obvious way to do it_

* Universality - general purpose:
  * Web, services, game logic, math, science, education
  * except DBs and things that required super fast computing

## Pluses/Minuses of Python: {#Pluses/Minuses-of-Python:}

### Pluses: {#Pluses:}

* Understandable tracebacks
* Pretty fast for it's tasks - web, UI, math, analyse \(PyPy, numpy, scipy\)
* Community \(for FullStackOverflow developers\)
* Ducktyping
* Tons of packages

\* Ducktyping - some common behavior of different object.

### Minuses: {#Minuses:}

* No JIT
  * In Python code is executed after pre-compilation \(bytecode creation\)
* Not fast compared to C, Rust, Java, Go and more memory-hungry
* Python object realization is costly
* Problems with concurrency \(Global Interpreter Lock\)
* Problems with sandboxing

### Why Python slower then compiled languages? {#Why-Python-slower-then-compiled-languages?}

1. Python is Dynamically Typed rather than Statically Typed.
   ![](/assets/static_dynamic.png)
2. Python is interpreted rather than compiled. A smart compiler can look ahead and optimize for repeated or unneeded operations, which can result in speed-ups
3. Python's object model can lead to inefficient memory access

### Comparison Python with other languages {#Comparison-Python-with-other-languages}

* Java

Python programs are generally expected to run slower than Java programs, but they also take much less time to develop. Python programs are typically 3-5 times shorter than equivalent Java programs. This difference can be attributed to Python's built-in high-level data types and its dynamic typing. For example, a Python programmer wastes no time declaring the types of arguments or variables, and Python's powerful polymorphic list and dictionary types, for which rich syntactic support is built straight into the language, find a use in almost every Python program. Because of the run-time typing, Python's run time must work harder than Java's. For example, when evaluating the expression a+b, it must first inspect the objects a and b to find out their type, which is not known at compile time. It then invokes the appropriate addition operation, which may be an overloaded user-defined method.

* C++

Almost everything said for Java also applies for C++, just more so: where Python code is typically 3-5 times shorter than equivalent Java code, it is often 5-10 times shorter than equivalent C++ code! Anecdotal evidence suggests that one Python programmer can finish in two months what two C++ programmers can't complete in a year. Python shines as a glue language, used to combine components written in C++.

## Python 2/3 {#Python-2/3}

There are two main branches of Python:

* Python 2 \(~ 2.7.10\)
* Python 3 \(~ 3.5.2\)

Nowadays most development \(especially new projects\) are started mostly on Python 3.

New \(and fixed old\) modules/technologies - are again mostly created firstly for Python 3 and in some cases backported.

Differences are not so big in general syntax so it's better to use Python 3 but be aware of differences and be able to understand both.

### Changes in print: {#Changes-in-print:}

| Python 2 | Python 3 | Result |
| :--- | :--- | :--- |
| print | print\(\) | **\r\n**\(empty line\) |
| print "Hi!" | print\("Hi!"\) | **Hi!** |
| print "Hi!", | print\(" Hi! ", end=""\) | **Hi!**\(no \r\n at the end\) |
| print "2 + 2 =", 2+2 | print\("2 + 2 =", 2\*2\) | **2 + 2 = 4** |
| N/A | print\(1, 2, 3, sep="--"\) | **1--2--3**\(with seperator\) |

Additionally:

* Many methods don't return lists \(results are iterators now\):
  * dict.keys\(\), dict.items\(\), dict.values\(\)
  * map\(\), filter\(\), zip\(\)
  * range\(\) = xrange\(\) from Python 2
* Iterator protocol change: next\(\) -&gt; \_\_next\_\_\(\)
* str = unicode
* Different types objects comparison \(you can't compare str and int\)
* PEP8 fixes

Bonus:

Bonus:

* Annotations

  ```py
  def foo(a: 'x', b: 5 + 6, c: list) -> max(2, 9)
  ```

* Cool unpacking:

  ```py
  (a, *rest, b) = range(5)
  ```

* New **super\(\) **– you don't need to write what class to extend \(we'll learn about them in OOP section\)

* Asyncio \(versions 3.4, 3.5+\)

### Python interpreter {#Python-interpreter}

* Interpreter - mean it runs code almost "live"
* Downloadable from [http://python.org](http://python.org)
* Python is script language but still it compiles runtime code in a form of so called bytecode which Python Virtual Machine \(PVM\) runs \(just like Java does with it's JVM\):

![](/assets/interpreter.png)

* Compiled code is auto-created and stored in .pyc files \(for Python 3 they are in separate \_\_pycache\_\_ directory\)

#### Ways of running Python script: {#Ways-of-running-Python-script:}

* Interactive shell \(UNIX/Windows\):

  ```
  $ python
  ```

* Run script:

  ```
  $ python script.py
  ```

* Run inline script:

  ```py
  $ python –c "print('Hello World yo!')"
  ```

# Basic syntax {#Basic-syntax}

## Identations {#Identations}

Identation or TAB, 2/4 spaces - whitespaces used to delimit program blocks - instead of punctuation or keywords, it uses indentation to indicate the run of a block.

```py
for i in [1, 2, 3]:
    if i == 3:
        print("Number 3 found!")
    else:
        print("Number:", i)
```

In C we need to use brackets\("{" and "}"\) to delimit blocks of code:

```cpp
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

In Python the same role is after indentations which make code much easier to read:

```py
def foo(x):
    if x == 0:
        bar()
        baz()
    else:
        qux(x)
        foo(x - 1)
```

Easter egg describing the "love to braces":

```py
>>> from __future__ import braces
File "<ipython-input-1-7e6f149a161c>", line 2
    from __future__ import braces
SyntaxError: not a chance
```

Indentation must maintain the constant level for same level of nesting.

This is **correct**:

```py
if condition:
    do_something1()
    do_something2()
```

This is **incorrect**:

```py
if condition:
    do_something1()
        do_something2()
```

If code block is not big it is allowed to use inline form:

```py
if condition: do_something1()
else: do_something2()
```

And it is possible to specify few statements on the same line using`;`:

```py
a = [x for x in range(10) if x % 2]; f = open("tmp.txt", "w"); f.write(a); f.close()
```

These two examples are not readable so used very rarely.

## Identificators and reserved words {#Identificators-and-reserved-words}

Naming rules:

* can have only alphabetical characters, numbers and `_`
* can't start with number
* case sensitive
* can't be one of reserved keywords

Reserved words \(which can't be used as variable names\):

```
and       del       from      not       while    
as        elif      global    or        with     
assert    else      if        pass      yield    
break     except    import    print              
class     exec      in        raise              
continue  finally   is        return             
def       for       lambda    try
```

### Comments and documentation strings {#Comments-and-documentation-strings}

`#`- starting with this symbol everything till the end of line is ignored

```
a = 12345  # This is comment
# This is comment too
# Continuing our comments
```

Doc string - first unassigned to variable string of module, function or class. These string are used by IDEs, help auto-generating scripts etc. It is possible to specify multiline string by using starting and ending with triple quotes\(`"""`or`'''`\).

```py
def f():
    '''
    Some nice function (the best in the world)

    :no params:
    :return: None
    '''
```

```py
>>> help(f)
Help on function f in module __main__:

f()
    Some nice function (the best in the world)

    :no params:
    :return: None
```

Or:

```py
>>> f.__doc__
'\n    Some nice function (the best in the world)\n    \n    :no params:\n    :return: None\n    '
```

## Objects in Python {#Objects-in-Python}

```py
a = 42
```

**a **is variable

**42 **is object of type **int**\(integer\)

* Variable - pointer to a object
* Object - specific structure in memory

So: variable holds a value. You can change the value of a variable at any point. In this case variable will just point to another object. Old object will remain but if it won't be referenced by any variable it will be cleaned out.

### Naming rules {#Naming-rules}

* Variables can only contain letters, numbers, and underscores. Variable names can start with a letter or an underscore, but can not start with a number.
* Spaces are not allowed in variable names, so we use underscores instead of spaces. For example, use student\_name instead of "student name".
* You cannot use Python keywords as variable names.
* Be careful about using the lowercase letter l and the uppercase letter O in places where they could be confused with the numbers 1 and 0.

#### Python Objects. Short explanation: {#Python-Objects.-Short-explanation:}

Everything in python is object. This includes basic types like strings, integers, lists and also - functions, classes, modules etc. Even type itself is object of class "type".  
Each object has:

* id \(address in memory\)
* type \(type object describing what kind this object is\)
* value \(some data pay-load\)

A lot of variables can point to same object. You don't need to declare what exact type variable should be.

* Compare objects by value:
  `==`
* Compare objects by id:
  `is`

#### Python Objects. In-depth details: {#Python-Objects.-In-depth-details:}

All Python objects are special structures in memory mostly consisting of the following attributes:

* reference counter \(how many variables or other links to this object exists, when it is 0 garbage collector will purge this object\)
* type \(pointer to another object that has information about type of current object\)
* some additional contextual data
  * for digits like int, float etc. - it's the value itself
  * for sequences - pointer to sctucture in memory which holds member objects

This is what happenes when you do`a = 42`- you bind name`a`from namespace to an object`42`. A namespace is a mapping from names \(identifiers\) to objects. You can rebind that name to another object \(even different type than previous\) - this called rebinding. Also that name can be unbindinned by`del a`.

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

## Installation, IDEs etc. {#Installation,-IDEs-etc.}

* Python.org:
  * [https://www.python.org/downloads/](https://www.python.org/downloads/)
* Pip \(already installed in new versions of Python\) is Python package manager:

  ```
  pip install jupyter virtualenv
  ```

* Virtualenv - manager of virtual environments which allows to keep different version of Python with different version of packages. Usage:

  ```
  virtualenv -p /path/to/existing/python venv
  source venv/bin/activate   # Unix
  venv\Scripts\activate      # Windows
  ...
  deactivate
  ```

### Problems with Python installation on Windows {#Problems-with-Python-installation-on-WIndows}

Mostly problems are related to incorrectly ENV variables. Some links with help to deal with this:

* [https://docs.python.org/2.7/using/windows.html](https://docs.python.org/2.7/using/windows.html)
* [https://docs.python.org/3/using/windows.html](https://docs.python.org/3/using/windows.html)

### Can't install some module via pip {#Can't-install-some-module-via-pip}

Sometimes to install additional package is impossible to do via pip because some pre-installed libraries \(like MS Studio C++ or mysql/postgresql libraries\) needed. So it's better to download and install precompiled packages from here:

* [http://www.lfd.uci.edu/~gohlke/pythonlibs/](http://www.lfd.uci.edu/~gohlke/pythonlibs/)

## Installation, IDEs etc. {#Installation,-IDEs-etc.}

### Best IDEs: {#Best-IDEs:}

* PyCharm \(Community Edition is OK\)
* Microsoft Visual Studio Code
* Sublime Text
* Eclipse with pydev
* Notepad++

# Sources for self-learning {#Sources-for-self-learning}

* Best and simplest possible interactive tutorial:
  * [http://www.learnpython.org/](http://www.learnpython.org/)
* Super detailed official Python tutorial \(a bit large\):
  * [https://docs.python.org/3/tutorial/](https://docs.python.org/3/tutorial/)
* List of links, tutorials on Habrahabr:

  * [http://habrahabr.ru/post/31180/](http://habrahabr.ru/post/31180/)

* Why Python slow? \(nice article with lot of Python internals explanation\)

  * [https://jakevdp.github.io/blog/2014/05/09/why-python-is-slow/](https://jakevdp.github.io/blog/2014/05/09/why-python-is-slow/)

Courses/Books:

* Think Python
  * [http://greenteapress.com/wp/think-python/](http://greenteapress.com/wp/think-python/)
* [http://learnpythonthehardway.org/book/](http://learnpythonthehardway.org/book/)
* [http://www.codecademy.com/tracks/python](http://www.codecademy.com/tracks/python)
* [https://www.coursera.org/course/pythonlearn](https://www.coursera.org/course/pythonlearn)

Tasks/Challenges:

* [http://www.codewars.com](http://www.codewars.com)
* [http://www.checkio.org](http://www.checkio.org)
* [http://empireofcode.com](http://empireofcode.com)



