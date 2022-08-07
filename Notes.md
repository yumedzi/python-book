# Notes about this Book

### Code

This book is the result of semi-manual conversion from [Jupyter notebooks](http://jupyter.org/) which show dynamic result of presented code executed. That's why sometimes you will see the code itself, for example:

```py
def mult(a, b=5): 
    return a * b
```

This represents regular Python code as you would write in your IDE. You can simply copy it and use in your program or run in Python interactive session after pasting it there.

To show that we are running some code and receiving output sometimes I will use `>>>` before actual command run so you could understand that the very next lines are result of previous command:

```py
>>> mult(4, 10)
40
```

Those `>>>` are exactly the same ones used in usual Python interactive session.

### Code output
So, in other words - presented code will be shown in two variations:

* Two sections - code and it's output separated:

```python
def splitting_function(text):
    return text.split()
text_to_split = "Hello Galaxy!"
splitting_function(text_to_split)
```

📟 _<mark style="color:green;">Output:</mark>

     ["Hello", "Galaxy!"]

* Code with output together \(code will be prefixed with &gt;&gt;&gt; \):

```python
>>> "Hello Universe!".split()
["Hello", "Universe!"]
```

### Hometasks

Originally course comes with a lot of home tasks. But for now they all are integrated in Training Suite companion web application. 

### Comments, propositions

If you find any error, flaw, incorrectness or have any other comment - please send my via email or Skype.

* email: `vityok(AT)gmail.com`
* skype: `lookinglass`

