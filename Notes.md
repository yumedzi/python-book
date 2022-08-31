# Notes about this Book

### Code (without results)

> All highlighted code you see across the book is the raw Python code. By default it doesn't have label if the code sample doesn't have any results presented.

This book is the result of semi-manual conversion from [Jupyter notebooks](http://jupyter.org/) which show dynamic result of presented code executed. That's why sometimes you will see the formatted and highlighted Python code itself, for example:

```python
def mult(a, b=5): 
    return a * b
```

This represents regular Python code as you would write in your IDE. You can simply copy it and use in your program or run in Python interactive session after pasting it there.

### Code with results

> To show the code + it's results I am using labels before code or output blocks across the books to help differentiate between them (because of `GitBook` enforced formatting previously it was hard to understand where is the code and where is it's results).

The presented code together with it's results/output will be shown in two variations:

* Code with output together (code will be prefixed with `>>>`):

To show that we are running some code and receiving output sometimes I will use `>>>` before actual command run so you could understand that the very next lines are results of the previous command(s):

🪄 <mark style="color:red;">Code</mark> <mark style="color:blue;">>>></mark> and <mark style="color:green;">📟</mark> <mark style="color:green;">Output</mark>:

```python
>>> "Hello Universe!".split()
["Hello", "Universe!"]
```

Those `>>>` are exactly the same ones used in usual Python interactive session (that you can invoke via running `python` in the terminal/shell).

* Two sections - code and it's output separated:

🪄 <mark style="color:red;">Code</mark>:



```python
def splitting_function(text):
    return text.split()
text_to_split = "Hello Galaxy!"
print(splitting_function(text_to_split))
```

📟 <mark style="color:green;">Output</mark>:

     ["Hello", "Galaxy!"]


### Hometasks

Originally course comes with a lot of hometasks. But for now they all are integrated in `Training Suite` companion web application. 

### Comments, propositions

If you find any error, flaw, incorrectness or have any other comment - please send my via email or Skype or Slack.

* 📧 Email: `vityok🐱gmail.com`
* 🇸 Skype: `lookinglass`

