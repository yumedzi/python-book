### Formatting

> There are two (old one new) styles of string formatting in Python. They are very similar when dealing with simple stuff but also have a lot of in-deep presentation and text transformation options

1. `printf-style` (**%**, old) - based on C printf style formatting that handles a narrower range of types and is slightly harder to use correctly, but is often faster for the cases it can handle.
2. `str.format()` (new) provides a large degree of flexibility and customization.
3. `f-strings` (Python 3.6) - inline formatting allowing to insert variables by names with format similar to `format()`


```python
print_me = 100505050.12123
print(  "1. %s" % print_me )         # Old format, %
print(  "2. {}".format(print_me) )   # New format, format()
print( f"3. {print_me}" )            # f-strings
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>1. 100505050.12123
    2. 100505050.12123
    3. 100505050.12123</code></span>


#### **%** (printf-style formatting)

> `format % values`

> `format` is a string, `%` conversion specifications in format are replaced with zero or more elements of `values`. 

A conversion specifier contains two or more characters and has the following components, which must occur in this order:

`1`. The '%' character - the start of the specifier.

`2`. Mapping key (optional), key name in parentheses (for example: `(somename)`).

`3`. Conversion flags (optional), which affect the result of some conversion types.

`4`. Minimum field width (optional). If specified as an '`*`' (asterisk), the actual width is read from the next element of the tuple in values, and the object to convert comes after the minimum field width and optional precision.

`5`. Precision (optional), given as a '`.`' (dot) followed by the precision. If specified as '`*`' (an asterisk), the actual precision is read from the next element of the tuple in values, and the value to convert comes after the precision.

`6`. Length modifier (optional).

`7`. Conversion type.



```python
food = "Ceasar salad"
print("For breakfast today is %s" % food)
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>For breakfast today is Ceasar salad</code></span>



```python
food = "Pizza Pepperoni and burger"
money = 130.23
print( "For lunch we have: %35s, budget: %012.3f UAH" % (food, money) )
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>For lunch we have:          Pizza Pepperoni and burger, budget: 00000130.230 UAH</code></span>



```python
data = {"food": "Pasta Carbonara", "money": 300}
print( "And for dinner:  %(food)20s, money to spend: %(money)9.2f UAH" % data )
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>And for dinner:       Pasta Carbonara, money to spend:    300.00 UAH</code></span>


#### **{}** / format()

It's better to use this for something that requries more complex formatting

> Format strings contain “replacement fields” surrounded by curly braces {}. Anything that is not contained in braces is considered literal text, which is copied unchanged to the output. If you need to include a brace character in the literal text, it can be escaped by doubling: {{ and }}.



```python
print("Our food today is {}".format(food))
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Our food today is Pizza Pepperoni and burger</code></span>


Several arguments:


```python
print("Food: '{}', money: {} UAH".format(food, money))
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Food: 'Pizza Pepperoni and burger', money: 130.23 UAH</code></span>


It is possible when using new format (_format()_) to specify positions:


```python
print("Food is {1}, money: {0}, (I have exactly ${0} in my wallet!)".format(money, food))
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Food is Pizza Pepperoni and burger, money: 130.23, (I have exactly $130.23 in my wallet!)</code></span>


It is possible to pass arguments by names:


```python
data = {"money": 45, "food":"salad"}
# `**` - means we are passing dict as a sequence of key-value pairs
print("Want {food} but ${money} to spend".format(**data))
# print("Want {food} but ${money} to spend".format(money=45, food="salad"))
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Want salad but $45 to spend</code></span>


More examples:


```python
"First thing in the morning is {0}".format("coffee") # References first positional argument
```




    'First thing in the morning is coffee'




```python
"I'd like a {} with coffee".format("cookie") # Implicitly references the first positional argument
```




    "I'd like a cookie with coffee"




```python
"Bring me {} and {}".format("coffee", "cookie") # Same as "From {0} to {1}"
```




    'Bring me coffee and cookie'




```python
"Remember my name: {name}".format(name="Heisenberg") # References keyword argument 'name'
```




    'Remember my name: Heisenberg'




```python
data = dict(do_what="Remember", my_what="name", name="Heisenberg")
"{do_what} my {my_what}: {name}".format(**data)
```




    'Remember my name: Heisenberg'




```python
"String has this method: {0.isalpha}".format("")  # 'isalpha' attribute of first positional arg
```




    'String has this method: <built-in method isalpha of str object at 0x7f2112e2dc70>'



### Differences between formatters:


| %               |  {}        | Output                                                                                        |
|-------------------------|----------------------|----------------------------------------------------------------------------|
|```'%s %s' % ('one', 'two')```    | ```'{} {}'.format('one', 'two')```    | ```one two```    |
| ```'%d %d' % (1, 2)```           | ```'{} {}'.format(1, 2)```            | ```1 2```        |
| ---                              | ```'{1} {0}'.format('one', 'two')```  | ```two one```    |
| ```'%10s' % ('test',)```         | ```'{:>10}'.format('test')```         | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```test``` | 
| ```'%-10s' % ('test',)```        | ```'{:10}'.format('test')```          | ```test```       |
| ---                              | ```'{:_<10}'.format('test')```       | ```test______``` |
| ---                              | ```'{:^10}'.format('test')```         | &nbsp;&nbsp;&nbsp;```test```&nbsp;&nbsp;&nbsp; | 

| %               |  {}        | Output                                                                                        |
|-------------------------|----------------------|----------------------------------------------------------------------------|
| ```'%.3s' % ('abcdef',)```       | ```'{:.3}'.format('abcdef')```        | ```abc```        | 
| ```'%d' % (42,)```               | ```'{:d}'.format(42)```               | ```42```         |
| ```'%06.2f' % (3.141592,)```     | ```'{:06.2f}'.format(3.14159)```      | ```003.14```     |
| ---                              | ```'{p.type}'.format(p=Plant())```    | ```tree```       |

In last example assuming p is the instance of Plant class defined like:
```python
class Plant(object):
    type = 'tree
```

#### .format() cheatsheet


| Data                    | Format                 | Output            | Decription |
|-------------------------|------------------------|------------------|-------------------------------------------------|
| ```3.1415926```         | ```{:.2f}```           | ```3.14```       | 2 decimal places    |
| ```3.1415926```         | ```{:+.2f}```          | ```+3.14```      |  2 decimal places with sign  |
| ```2.71828```           | ```{:.0f}```           | ```3```          | No decimal places    |
| ```1000000```           | ```{:,}```             | ```1,000,000```  |  Number with comma sep |
| ```13```                | ```{:>10d}```           | <code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code>`13`         | Right aligned 
| ```13```                | ```{:<10d}```          | `13`<code>&nbsp;&nbsp;&nbsp;&nbsp;</code>         | Left aligned |
| ```13```                | ```{:^10d}```          | <code>&nbsp;&nbsp;&nbsp;&nbsp;</code>`13`<code>&nbsp;&nbsp;&nbsp;&nbsp;</code>         | Center aligned |

#### .format() "cheats"
* Show the same string several times


```python
print('''{0}!
{1}. 
"{0}!" 
{1}. 
"What's gone with that boy, I wonder? You {0}!" {1}. 
'''.format('TOM', 'No answer'))

```

    TOM!
    No answer. 
    "TOM!" 
    No answer. 
    "What's gone with that boy, I wonder? You TOM!" No answer. 
    


* Convert Values to different Bases 
    * You can use the following letters to convert a number to their bases:
        * decimal, hex, octal, binary


```python
print ("{0:d} - {0:x} - {0:o} - {0:b}".format(21))
```

    21 - 15 - 25 - 10101


* Escaping braces:


```python
print ( "{{0}} / {}".format("TEST") )
```

    {0} / TEST


#### f-strings formatting

New feature appeared in Python 3.6. It is possible to inject local variable right into string (variable interpolation)

> Formatted string literals are prefixed with 'f' and are similar to the format strings accepted by str.format(). They contain replacement fields surrounded by curly braces. The replacement fields are expressions, which are evaluated at run time, and then formatted using the format() protocol

This feature is described by [PEP 498](https://www.python.org/dev/peps/pep-0498/#specification)



The format is:

```python
f'<text> { <expression> <optional !s, !r, or !a> <optional : format specifier> } <text> ... '
```


```python
var = 34.125
print(f'{var}')
print(f'{var:012.3f}')
print(f'{var:_^12.3f}')
print(f'{var:^10}')  
```

    34.125
    00000034.125
    ___34.125___
      34.125  


In case interpolating var is not defined - you'll get regular NameError:


```python
f'{unexistent_var}'
```


    

    NameErrorTraceback (most recent call last)

    <ipython-input-71-a2838fe909a3> in <module>
    ----> 1 f'{unexistent_var}'
    

    NameError: name 'unexistent_var' is not defined



```python
f'{1/0}'
```


    

    ZeroDivisionErrorTraceback (most recent call last)

    <ipython-input-72-a9fc87ed0d89> in <module>
    ----> 1 f'{1/0}'
    

    ZeroDivisionError: division by zero


`f-string` are evaluated only during creation (once):


```python
value = 100500
str_ = f'Value is {value}'

print(str_)
```

    Value is 100500



```python
value = 42
print(str_)
```

    Value is 100500


Expressions may be evaluated directly inside a string:


```python
f'{ 1 + 2 }'
```




    '3'




```python
f'{"just another string"}'
'quoted string'
```




    'quoted string'




```python
d = {"a": 100500}
l = [1, 2, 3, 4, 5]

f'{d["a"], l[2:5]}'
```




    '(100500, [3, 4, 5])'




```python
def foo(x): 
    return "Hello! %s" % x
print(f'Result of function is:\n{foo("John")}')
```

    Result of function is:
    Hello! John


Format int value as hex:


```python
value = 1234
f'input={value:#x}'
```




    'input=0x4d2'



Format `datetime` objects (see [docs for datetime formatting](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior):


```python
import datetime
now = datetime.datetime.now()
print(now.strftime("%a %d/%m/%Y"))
f'It was: {now:%a %d/%m/%Y}'
```

    Mon 01/03/2021





    'It was: Mon 01/03/2021'



### Dynamic width


```python
import decimal

width = 12
precision = 5
value = decimal.Decimal('12.34567')
f'result: {value:{width}.{precision}f}'
```




    'result:     12.34567'



####  Templates

A bit underrated feature of builtin string module. _Template_ is very simple template engine.


```python
from string import Template 
s = Template('$who likes $what')
print(s.substitute(who='Johnny', what='whiskey'))

d = dict(who='tim')
#Template('Give $who $cookie').substitute(d) <--- will raise KeyError as 'cookie' not in a dictionary
print(Template('$who likes $cookies').safe_substitute(d)) # proper way
```

    Johnny likes whiskey
    tim likes $cookies