# String Formatting

> There are two (old one new) styles of string formatting in Python. They are very similar when dealing with simple stuff but also have a lot of in-deep presentation and text transformation options

1. `str.format()` (new) provides a large degree of flexibility and customization.
2. `printf-style` (**%**, old) - based on C printf style formatting that handles a narrower range of types and is slightly harder to use correctly, but is often faster for the cases it can handle.
3. `f-strings` (Python 3.6) - inline formatting allowing to insert variables by names with format similar to `format()`


Example:
```python
print_me = "The World is Mine"
print(  "1. %s" % print_me )         # Old format, %
print(  "2. {}".format(print_me) )   # New format, format()
print( f"3. {print_me}")            # f-format
```

Output:
```
1. The World is Mine
2. The World is Mine
3. The World is Mine
``` 

## **%** (printf-style formatting)

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
>>> food = "Ceasar salad"
>>> print("For breakfast today is %s" % food)
For breakfast today is Ceasar salad
```

```python
>>> food = "Pizza Pepperoni and burger"
>>> money = 130.25
>>> "For lunch we have: %29s, budget: %10.3f UAH" % (food, money)
For lunch we have:    Pizza Pepperoni and burger, budget:    130.250 UAH
```

```python
>>> data = {"food": "Pasta Carbonara", "money": 300}
>>> "And for dinner:  %(food)20s, money to spend: %(money)s" % data
And for dinner:       Pasta Carbonara, money to spend: 300
```

## **{}** / format()

It's better to use this for something that requries more complex formatting

> Format strings contain “replacement fields” surrounded by curly braces {}. Anything that is not contained in braces is considered literal text, which is copied unchanged to the output. If you need to include a brace character in the literal text, it can be escaped by doubling: {{ and }}.



```python
>>> "Our food today is {}".format(food)
'Our food today is Pizza Pepperoni'
```

Several arguments:


```python
>>> "Food: '{}', money: {} UAH".format(food, money)
'Food: 'Pizza Pepperoni', money: 130.25 UAH'
```

It is possible when using new format (`.format()`) to specify positions:

```python
>>> "Food is {1}, money: {0}".format(money, food)
'Food is Pizza Pepperoni and burger, money: 130.25'
```

It is possible to pass arguments by names:

```python
>>> data = {"money": 45, "food":"salad"}
# `**` - means we are passing dict as a sequence of key-value pairs
>>> "Want {food} but ${money} to spend".format(**data)
# The same as:
# "Want {food} but ${money} to spend".format(money=45, food="salad")
'Want salad but $45 to spend'
```
More examples:

```python
>>> "First thing in the morning is {0}".format("coffee") # References first positional argument
'First thing in the morning is coffee'
```

```python
>>> "I'd like a {} with coffee".format("cookie") # Implicitly references the first positional argument
"I'd like a cookie with coffee"
```

```python
>>> "Bring me {} and {}".format("coffee", "cookie") # Same as "From {0} to {1}"
'Bring me coffee and cookie'
```

```python
>>> "Remember my name: {name}".format(name="Heisenberg") # References keyword argument 'name'
'Remember my name: Heisenberg'
```

```python
>>> data = dict(do_what="Remember", my_what="name", name="Heisenberg")
>>> "{do_what} my {my_what}: {name}".format(**data)
'Remember my name: Heisenberg'
```

```python
>>> "String has this method: {0.isalpha}".format("")  # 'isalpha' attribute of first positional arg
'String has this method: <built-in method isalpha of str object at 0x0000000000439AB0>'
```

## Differences between formatters:


| %               |  {}        | Output                                                                                        |
|-------------------------|----------------------|----------------------------------------------------------------------------|
|```'%s %s' % ('one', 'two')```    | ```'{} {}'.format('one', 'two')```    | ```one two```    |
| ```'%d %d' % (1, 2)```           | ```'{} {}'.format(1, 2)```            | ```1 2```        |
| ---                              | ```'{1} {0}'.format('one', 'two')```  | ```two one```    |
| ```'%10s' % ('test',)```         | ```'{:>10}'.format('test')```         | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```test``` | 
| ```'%-10s' % ('test',)```        | ```'{:10}'.format('test')```          | ```test```       |
| ---                              | ```'{:\_<10}'.format('test')```       | ```test______``` |
| ---                              | ```'{:^10}'.format('test')```         | &nbsp;&nbsp;&nbsp;```test```&nbsp;&nbsp;&nbsp; |
| ```'%.3s' % ('abcdef',)```       | ```'{:.3}'.format('abcdef')```        | ```abc```        | 
| ```'%d' % (42,)```               | ```'{:d}'.format(42)```               | ```42```         |
| ```'%06.2f' % (3.141592,)```     | ```'{:06.2f}'.format(3.14159)```      | ```003.14```     |
| ---                              | ```'{p.type}'.format(p=Plant())```    | ```tree```       |

In last example assuming p is the instance of Plant class defined like:
```python
class Plant(object):
    type = 'tree
```

### .format() cheatsheet


| Data                    | Format                 | Output            | Decription |
|-------------------------|------------------------|------------------|-------------------------------------------------|
| ```3.1415926```         | ```{:.2f}```           | ```3.14```       | 2 decimal places    |
| ```3.1415926```         | ```{:+.2f}```          | ```+3.14```      |  2 decimal places with sign  |
| ```2.71828```           | ```{:.0f}```           | ```3```          | No decimal places    |
| ```1000000```           | ```{:,}```             | ```1,000,000```  |  Number with comma sep |
| ```13```                | ```{:10d}```           | ```13```         | Right aligned 
| ```13```                | ```{:<10d}```          | ```13```         | Left aligned |
| ```13```                | ```{:^10d}```          | ```13```         | Center aligned |

### .format() "cheats"
#### Show the same string several times


```python
print('''{0}!
{1}. 
"{0}!" 
{1}. 
"What's gone with that boy, I wonder? You {0}!" {1}. 
'''.format('TOM', 'No answer'))```

Output:
```
    TOM!
    No answer. 
    "TOM!" 
    No answer. 
    "What's gone with that boy, I wonder? You TOM!" No answer. 
```    
    

#### Convert Values to different Bases 
You can use the following letters to convert a number to their bases:
        * **d**ecimal, he**x**, **o**ctal, **b**inary


```python
print ("{0:d} - {0:x} - {0:o} - {0:b} ".format(21))
```

Output:
```
21 - 15 - 25 - 10101 
``` 

#### Escaping braces:

```python
>>> print ( "{{0}} / {}".format("TEST") )
{0} / TEST
```
    

## f-strings formatting

New feature appeared in Python 3.6. It is possible to inject local variable right into string (variable interpolation)

> Formatted string literals are prefixed with 'f' and are similar to the format strings accepted by str.format(). They contain replacement fields surrounded by curly braces. The replacement fields are expressions, which are evaluated at run time, and then formatted using the format() protocol

This feature is described by [PEP 498](https://www.python.org/dev/peps/pep-0498/#specification)



The format is:

```python
f ' <text> { <expression> <optional !s, !r, or !a> <optional : format specifier> } <text> ... '
```


```python
var = 34.125
print(f'{var}')
print(f'{var:012.4}')
print(f'{var:^10}')
   
```
Output:

    34.125
    000000034.12
      34.125  
    

In case interpolating var is not defined - you'll get regular NameError:


```python
f'{unexistent_var}'
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-11-046bddf22923> in <module>()
    ----> 1 f'{unexistent_var}'
    

    NameError: name 'unexistent_var' is not defined


Expressions may be evaluated directly inside a string:


```python
>>> f'{ 1 + 2 }'
'3'
```

```python
>>> f'{"just another string"}'
'quoted string'
```

```python
>>> d = {"a": 100500}
>>> f'{d["a"]}'
'100500'
```

It is possible to call a function inside f-string:

```python
def foo(x): 
    return "Hello! %s" % x
f'{foo("John")}'
```

Output:

    'Hello! John'

Convert to hex (or other base):
```python
>>> value = 1234
>>> f'input={value:#06x}'
'input=0x04d2'
```

```python
>>> import datetime
>>> date = datetime.date(2017, 1, 1)
>>> f'{date} was on a {date:%A}'
'2017-01-01 was on a Sunday'
```

### Dynamic width

```python
import decimal

width = 10
precision = 4
value = decimal.Decimal('12.34567')
f'result: {value:{width}.{precision}}'
```
Output:

    'result:      12.35'

##  Templates

A bit underrated feature of builtin string module. _Template_ is very simple template engine.


```python
>>> from string import Template 
>>> s = Template('$who likes $what')
>>> print(s.substitute(who='Johnny', what='whiskey'))
Johnny likes whiskey

>>> d = dict(who='tim') 
>>> #Template('Give $who $cookie').substitute(d) <--- will raise ValueError as 'cookie' not in a dictionary
>>> print(Template('$who likes $cookies').safe_substitute(d)) # proper way
tim likes $cookies
```