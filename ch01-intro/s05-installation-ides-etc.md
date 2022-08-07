## Installation, IDEs etc.

* Python.org: 
    *  https://www.python.org/downloads/ 

* Pip (already installed in new versions of Python) is Python package manager.
* Conda (Miniconda):
    * https://docs.conda.io/en/latest/miniconda.html

Main commands:

* install package (install requirements from a file):

    ```bash
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
pip install jupyter virtualenv
pip install -r requirements.txt
```
```
{% endcode %}

* uninstall package:
    ```bash
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
pip uninstall requests
```
```
{% endcode %}

* list all installed packages:
    ```bash
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
pip freeze
pip freeze > requirements.txt
```
```
{% endcode %}

### Virtualenv 

**virtualenv** - virtual environment creation tool which allows to keep different version of Python with different version of packages. Usage:

```sh
virtualenv -p /path/to/existing/python venv
source venv/bin/activate   # Unix
venv\Scripts\activate      # Windows
...
deactivate
```

### virtualenvwrapper

Better tool to manage different python virtual environment is virtualenvwrapper.

* UNIX:
    * [virtualenvwrapper site](https://virtualenvwrapper.readthedocs.io/en/latest/)
* Windows clone:
    * [virtualenvwrapper-win](https://github.com/davidmarble/virtualenvwrapper-win/)
    
> Main feature is controlling all available environments with easy fast switching between them.

Installation:

`pip install virtualenvwrapper` (or `pip install virtualenvwrapper-win`)

There are two related terms: projects and virtual environments.

* Virtual environment
    * Environment that lives inside `$WORKON_HOME` (`%WORKON_HOME%`)
* Project
    * Directory with the code related to specific venv. 
    * If venv was created with association to specific project dir (`-a <path/to/project/`) - after switching to it virtualenvwrapper will chande current directory to project. 
    

**virtualenvwrapper** VENV commands:

* Create new venv:
    * `mkvirtualenv [mkvirtualenv-options] [virtualenv-options] VENV_NAME`
    * mkvirtualenv options:
       *  `-a project_path`       Associate existing path as project directory
       *  `-i package`            Install package in new environment
       *  `-r requirements_file`  
       * `VENV_NAME` (must be last) - the name of resulted venv
* List of all venvs:
    * `workon` **RECOMMENDED**
    * `lsvirtualenv`
* Switch to another venv:
    * `workon VENV_NAME`
* Deactivate current venv:
    * `deactivate`

**virtualenvwrapper** PROJECTS commands:

* Associate project with current active venv:
    * `setprojectdir <path/to/project/>`

* Create new project environment:
    * `mkproject`
        * If the environment variable `$PROJECT_HOME` (`%PROJECT_HOME%`) is set, create a new project directory in PROJECT_HOME
* Change into project directory:
    * `cdproject`
    * `cd-` - change into the directory you were before running `cdproject`

### How to add existing virtualenv to virtualenvwrapper

Easiest way is to dump all packages from `virtualenv` environment and recreate with `virtualenvwrapper`:

```sh

# dumping part
cd /home/user/projects/old_project/
source .venv/bin/activate (`.venv` is the dir with venv)
pip freeze > requirements.txt
which python > python_bin.txt
deactivate
rm -rf .venv

# virtualenvwrapper part
mkvirtualenv -a /home/user/projects/old_project/ -p `cat python_bin.txt` -r requirements.txt SOME_PROJ
```



### Problems with Python installation on Windows

Mostly problems are related to incorrectly ENV variables. Some links with help to deal with this:

* https://docs.python.org/2.7/using/windows.html 
* https://docs.python.org/3/using/windows.html 

### Can't install some module via pip

Sometimes to install additional package is impossible to do via pip because some pre-installed libraries (like MS Studio C++ or mysql/postgresql libraries) needed. So it's better to download and install precompiled packages from here:

* http://www.lfd.uci.edu/~gohlke/pythonlibs/

Install of .whl package:

```sh
pip install <whl_file>
```

### Problem with installing packages on Windows: Microsoft Visual C++ is missing

When you see this during installing some package with pip:

```sh
...
    error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": https://visualstudio.microsoft.com/downloads/
```

this means it is required to download and install **Microsoft Visual C++ Build Tools**:

* go to [Downloads page](https://visualstudio.microsoft.com/downloads/) > "Tools for Visual Studio 2019"
* Download and run installer for `Build Tools for Visual Studio 2019`
* Select checkbox for `Build Tools` and click "Install"

## Best IDEs:

* Microsoft Visual Studio Code
* PyCharm (Community Edition is OK)
* Sublime Text
* Eclipse with pydev
* Notepad++
* vim