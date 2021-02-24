## Ipython

> `ipython` is part of [`Jupyter`](https://jupyter.org/) project.
Ipython is enhanced version of Python shell. It is also "REPL" shell. This means:

* **Read**: take user input.
* **Eval**: evaluate the input.
* **Print**: shows the output to the user.
* **Loop**: repeat.

<img src="../images/jupyter_logo.png">



Main features of `ipython`:

* Autocompletion
    * Completion with `TAB` for python's builtin functions and existing variables
* Syntax highligthing
* Object introspection
    * Help for object (object with `__doc__` which is used for Python's `help()`) - `obj?`
    * List of object's methods/attributes - `object_name.<TAB>`
    

### Running and Editing

The `%run` magic command allows you to run any python script and load all of its data directly into the interactive namespace. Since the file is re-read from disk each time, changes you make to it are reflected immediately (unlike imported modules, which have to be specifically reloaded). IPython also includes `dreload`, a recursive reload function.

`%run` has special flags for timing the execution of your scripts (`-t`), or for running them under the control of either Python’s pdb debugger (`-d`) or profiler (`-p`).

The `%edit` command gives a reasonable approximation of multiline editing, by invoking your favorite editor on the spot. IPython will execute the code you type in there as if it were typed interactively.

It is possible to search the previously entered code with `Ctrl-R` shortcut.

### History

IPython stores both the commands you enter, and the results it produces. You can easily go through previous commands with the up- and down-arrow keys, or access your history in more sophisticated ways.

Input and output history are kept in variables called In and Out, keyed by the prompt numbers, e.g. `In[4]`. The last three objects in output history are also kept in variables named `_`, `__` and `___`.

You can use the `%history` magic function to examine past input and output. Input history from previous sessions is saved in a database, and IPython can be configured to save output history.

### System shell commands

To run any command at the system shell, simply prefix it with !, e.g.:


```python
!pwd
```

    /notebooks


### Ipython magic functions

IPython has a set of predefined "magic functions" that you can call with a command line style syntax. 

There are two kinds of magics, line-oriented and cell-oriented. Line magics are prefixed with the % character and work much like OS command-line calls: they get as an argument the rest of the line, where arguments are passed without parentheses or quotes. Cell magics are prefixed with a double %%, and they are functions that get as an argument not only the rest of the line, but also the lines below it in a separate argument.

The following examples show how to call the builtin %timeit magic, both in line and cell mode:





```python
%timeit range(1000)
```

    502 ns ± 4.41 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)



```python
%%timeit x = range(10000)
max(x)
```

    609 µs ± 2.23 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)


The builtin magics include:

* Functions that work with code: `%run`, `%edit`, `%save`, `%macro`, `%recall`, etc.
* Functions which affect the shell: `%colors`, `%xmode`, `%autoindent`, `%automagic`, etc.
* Other functions such as `%reset`, `%timeit`, `%%writefile`, `%load`, or `%paste`.


To see all available magics:

* `%lsmagic`