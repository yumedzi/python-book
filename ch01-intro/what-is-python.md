# What is Python?

Python is high-level dynamically typed interpreted programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than would be possible in languages such as C++ or Java.

> _There should be one — and preferably only one — obvious way to do it_

* Universality - general purpose:
  * Web, services, game logic, math, science, education
  * except DBs and things that required super fast computing

### Canonical example {#Canonical-example}

```py
>>> print("Hello World!!")
Hello World!!
```

For Python 2:

```py
>>> print "Hello World"
Hello World
```

## There is an Easter egg illustrating Python's core idea: {#What-is-Python?}

```
>>> import antigravity
```

![](/assets/antigravity.png)

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



