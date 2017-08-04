
# Namespaces

Namespaces are just dictionaries with some names (what we call variable name) mapped to objects (actual data in memory). This mapping mapping allows to access target object by a name that we've assigned to it. So: 
```python
some_string = "Hello World"
```
creates a reference to the "Hello Worold" object, and makes it accessible by variable name ```some_string```.

In this case our namespace will be:
```python
{"some_string": "Hello World"}
```

In Python it's possible to have multiple namespaces (for example: each function has it's own context). When we trying to get some variable inside some namespace Python firstly looks at so-called local namespace and if it is not found it goes "upper". Such local contextual namespaces in Python called "scopes".
