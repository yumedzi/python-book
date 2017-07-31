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

### PIP {#Problems-with-Python-installation-on-WIndows}

> PIP is Python modern 3rd party module manager which based on it's own DB of published modules. It is pre-installed for Python 2 &gt;=2.7.9 or Python 3 &gt;= 3.4.

PIP quickstart is [here](https://pip.pypa.io/en/stable/quickstart/).

Main commands:

* `pip freeze`, `pip list` - see all installed packages
* `pip install <module>` - install new package
* `pip uninstall <module>` - deinstall some package

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



