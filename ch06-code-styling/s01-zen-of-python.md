# Zen of Python

Also know as PEP 20. (PEP is proposal for enhancement)


```python
import this
```

<div><pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>The Zen of Python, by Tim Peters</code></pre></div>
    
    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!


## Zen of Python (summary)

* Readability is very important
    * 10 reads, 1 write
* Simple is better than complex
    * Easier to maintain and upgrade
* Motivations:
    * Beautiful code
    * "Pythonic way"


Update/clean advises

## General advises

* Use docstrings in modules and functions, add `README.md` to your project
* Don't use inline comments too much - clear code is better than comment.
* Split your code into small functions. Ideal length - less than 10 lines. 
* Variables should be lower-case with underscores `all_lines` and not `AllLines` or `allLines`. 
* Variables should be named properly with descriptive names( `a`, `abc` or `function_1` are not good). 
* Modules ( `.py` files) should be max 500 lines of code. 
* Each module should have a clear purpose and name (e.g. `data_processing.py`, `db_export.py` ). 
* Use `if name == '__main__':` code blocks if this module will be imported. 
* Use list comprehensions when it is suitable (not too long lines)
* Use `for` loops and don't forget about `continue` and `break/else` clauses. 
* When iterating - don't use `for i in range(len(list_))`, use `enumerate()` instead