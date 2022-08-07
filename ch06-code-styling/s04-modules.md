# Modules

> Python module is a single file that can be imported using `import`

Basically, it's just a synonim for a "script".

Definitions from a module can be imported into other modules or into the `main` module (the collection of variables that you have access to in a script executed at the top level and in interactive mode (`python` or `ipython`)).

Why do we need them?
* To split the the code into several files for easier maintenance

What can be imported:
* variables
* functions
* classes

A module can contain executable statements as well as function definitions. These statements are intended to initialize the module. They are executed only the first time the module name is encountered in an `import` statement.

## Import

🪄 _<mark style="color:green;">Code:</mark>_

```python
import foo                  # foo imported and bound locally
import foo.bar.baz          # foo.bar.baz imported, foo bound locally
import foo.bar.baz as fbb   # foo.bar.baz imported and bound as fbb
from foo.bar import baz     # foo.bar.baz imported and bound as baz
from foo import attr        # foo imported and foo.attr bound as attr
from foo import *           # everything from foo -> curr. namespace
```

Example

**helpers.py:**

```python
import math

def circle_area(x):
    return math.pi * x * x

def sector_area(r, a):
    return circle_area(r) * a / 360
```

**code.py**:

```python
import helpers
from helpers import sector_area as sa

print(helpers.circle_area(2))
print(sa(2, 30))
```

Module search logic:
* built-in + already imported modules, `sys.modules`
* files with the same name in current directory
* locations in PYTHONPATH (`sys.path`):
    * the directory containing the input script (or the current directory).
    * PYTHONPATH (a list of directory names, with the same syntax as the shell variable PATH). 
    * the installation-dependent default.

`__name__` - global variable that contains the module’s name (as a string)


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(__name__)
```

📟 _<mark style="color:green;">Output:</mark>_

    __main__


Execution of modules as scripts:

🪄 _<mark style="color:green;">Code:</mark>_

```python
if __name__ == "__main__":
    # Do something
    import sys
    print(sys.__name__)
```

After initialization, Python programs can modify sys.path. The directory containing the script being run is placed at the beginning of the search path, ahead of the standard library path.

```python
import sys
print(sys.path)
sys.path.append('/opt/prog/modules')

import some_module
```

## Reimporting

Using import module again will not reload it, it will just re-read it from cache.

* Use the following to reload:

🪄 _<mark style="color:green;">Code:</mark>_

```python
#import imp # Deprecated in 3.4.0
import importlib as imp
imp.reload(module)
```

Python module's code is recompiled and the module-level code reexecuted. The init function of extension modules is not called a second time. As with all other objects in Python the old objects are only reclaimed after their reference counts drop to
zero. The names in the module namespace are updated to point to any new or changed objects.

## Compiled Python files

As an important speed-up of the start-up time for short programs that use a lot of standard modules, if a file called `spam.pyc` exists in the directory `__pycache__` where `spam.py` is found, this is assumed to contain an already-“byte-compiled” version of the module `spam`. (For Python2 those `.pyc` files were located in the same directory as `.py` files).

The modification time of the version of spam.py used to create spam.pyc is recorded in spam.pyc, and the .pyc file is ignored if
these don’t match. The contents of the spam.pyc file are platform independent, so a Python module directory can be shared by machines of different architectures.

A program doesn’t run any faster when it is read from a `.pyc` or `.pyo` file than when it is read from a .py file; the only thing that’s faster about `.pyc` or `.pyo` files is the speed with which they are loaded. Only profit is a time of compilation!

# Standard modules

Python comes with a library of standard modules, described in a separate document, the Python Library Reference (“Library
Reference” hereafter). 

https://docs.python.org/3/library/

Some modules are built into the interpreter; these provide access to operations that are not part of the core of the language but are nevertheless built in, either for efficiency or to provide access to operating system primitives such as system calls.

## Very short overview of main modules

* OS-level
    * `os, sys, io, argparse, optparse, logging, curses, platform`
    * `ctypes, time, datetime, multiprocessing, threading, subprocess`
* String services:
    * `re, string, datetime, collections, pprint`
* Numbers/calculation:
    * `numbers, math, decimal`

* Cryptographic:
    * `hashlib, hmac`
* FP:
    * `functools, operator, itertools`
* Serializing and compression:
    * `pickle, json, shelve, marshal, dbm`
    * `sqlite3, zlib, bz2, zipfile, tarfile`

* Internet:
    * `smtp, email, mailbox, mimetools, base64, uu`
* Network:
    * `socket, selectors, asyncore, asyncio`
* Structured Markup Processing Tools
    * `HTMLParser, sgmllib, htmllib, xml.etree, xml.dom`
    * `urllib(2), (http|smtp|ftp|imap|ntp)lib`
* Development:
    * `pydoc, doctest, unittest, 2to3`