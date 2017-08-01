# Strings

> String is **immutable **sequence of characters. For Python it's almost like any other sequence \(more like tuple which is immutable version of list\). 
>
> In Python 3 all characters are unicode objects - abstract representation of some symbol. It is like an "idea" of a symbol. When printing or writing to file strings are encoded to bytes with default encoding automatically by Python.

String literals are written in a variety of ways:

* Single quotes:
  `'allows embedded "double" quotes'`
* Double quotes:
  `"allows embedded 'single' quotes".`
* Triple quoted:
  `'''Three single quotes''', """Three double quotes"""`

Examples: 

```py
>>> s1 = "Hello, I'm nice little string"
>>> s2 = 'Hello, I\'m nice little string'   # escaping '
>>> print(s1)
Hello, I'm nice little string

>>> print(s2)
Hello, I'm nice little string
```

Multi-line string \(matter of syntax, for Python they are all the same\):

```py
big_string = """Starting here
Going and going and going...
And again and again
... a bit bored..
I need to rest...
"""

print(big_string)
```

Output:

```
Starting here
Going and going and going...
And again and again
... a bit bored..
I need to rest...
```

### Main methods of strings {#Main-methods-of-strings}

In \[24\]:

```py
print(dir("some_string"))  # Emm... actually all methods...
```

Output with all methods of strings:

```py
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', 
'__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', 
'__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__',
'__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count',
'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 
'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust',
'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip',
'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```



| Method\(s\) | Description |
| :--- | :--- |
| `lower(), upper()` | Return new string - in lowercase, uppercase |
| `title(), capitalize()` | Return new string - with first world in uppercase, all words starts with uppercase |
| `isalpha(), isdigit(), isalnum()` | Return True/False - are all characters: chars, digits, alpha-numerical? |
| `isspace()` | Return True/False - are all characters whitespaces \(" ", "\n", "\t" etc.\) ? |
| `strip(), rstrip(), lstrip()` | Return new string with removed whitespaces |
| `count(s)` | Return number of sub-string **s **is part of string |
| `index(s)` | Return index of first sub-string **s **that found in a string |
| `split(s)` | Return list of string parts splitted by delimiter s \(" " by default\) |
| `replace(s, r)` | Return new string with all sub-strings**s**replaced by string **r** |
| `s in some_string` | Return True/False - check is sub-string**s**is part of **some\_string**? |
| `startswith(s), endswith(s)` | Return True/False - check is string starts or ends with a sub-string **s** |
| `s.join(list_of_strings)` | Return new string - result of merging all strings from list using delimiter **s** |
| `some_string[i]` | Return new string - one character by index **i** |
| `some_string[n1:n2:step]` | Return new string - sub-string from n1 till n2 \(non-inclusive\) with step **step** |
| `len(some_string)` | Return int - length of string |



#### Some examples {#Some-examples}

```py
some_string = "Some funny string!"
```

##### Adding, multiplying\(!\) strings {#Adding,-multiplying(!)-strings}

```py
>>> some_string + " and another string"
'Some funny string! and another string'
```

```py
>>> some_string * 3
'Some funny string!Some funny string!Some funny string!'
```

##### Get length {#Get-length}

```py
>>> len(some_string)
18
```

##### Cosmetical methods: {#Cosmetical-methods:}

* lower, upper, title, capitalize

```py
some_string.lower(), some_string.upper(), some_string.title(), some_string.capitalize()
```

Output:

```
('some funny string!',
 'SOME FUNNY STRING!',
 'Some Funny String!',
 'Some funny string!')
```

##### Various checking for lower/upper, all digits, all letters. Returns True/False. {#Various-checking-for-lower/upper,-all-digits,-all-letters.-Returns-True/False.}

```py
>>> some_string.islower(), some_string.isupper(), some_string.isdigit(), some_string.isalpha(), some_string.isalnum()
(False, False, False, False, False)
```

Yeah, yeah, it was boring example...

##### Nice examples regarding checks: {#Nice-examples-regarding-checks:}

```py
>>> low_str = "asdasdfhjksdhfjh"
>>> low_str.islower(), low_str.isupper()
(True, False)
```

```py
>>> almost_digit_str = "12123123 123123"
>>> true_digit_str = "12312387877987987"
>>> almost_digit_str.isdigit(), true_digit_str.isdigit()
(False, True)
```

```py
>>> phone_num = "066-749-99-99"
>>> name = "Johnny"  
>>> name_with_spaces = name + " Walker" # Note that whitespaces are not alpha!
>>> phone_num.isalpha(), name.isalpha(), name_with_spaces.isalpha()
(False, True, False)
```

##### Checking for space-containing strings {#Checking-for-space-containing-strings}

* To check for all-spaces string - use`.isspace()`

```py
>>> "    ".isspace(), "  \t \n  \r\n".isspace()
(True, True)
```

* A bit hackish way to check for alphabeticals with spaces - via using`.replace()`

```py
>>> "Hello World".replace(" ", "").isalpha()
True
```

##### Stripping - removing whitespaces {#Stripping---removing-whitespaces}

* `.strip()`
  - remove from the beginning and from the end both
* `.rstrip()`
  - remove only from the end
* `.lstrip()`
  - remove only from the beginning

Example:

```py
whitespaces_str = "  Some text goes and goes...  "
print("Initial string:   >>>" + whitespaces_str + "<<<")
print("Stripped string: >>>" + whitespaces_str.strip() + "<<<")
print("R-stripped string: >>>" + whitespaces_str.rstrip() + "<<<")
print("L-stripped string: >>>" + whitespaces_str.lstrip() + "<<<")
```

Output:

```
Initial string:   >>>  Some text goes and goes...  <<<
Stripped string: >>>Some text goes and goes...<<<
R-stripped string: >>>  Some text goes and goes...<<<
L-stripped string: >>>Some text goes and goes...  <<<
```

##### Get character by index \(it's possible because string is sequence\) {#Get-character-by-index-(it's-possible-because-string-is-sequence)}

Indexing starts from 0. Negative indexing means counting from the end so -1 is the last item.

```py
>>> some_string
'Some funny string!'

>>> some_string[0]
'S'

>>> some_string[3]
'e'

>>> some_string[-1]
'!'
```

##### Slicing {#Slicing}

`some_str[start:stop:step]`\(again sequence-like syntax\) - getting part of sequence.

* Returns items with indexes starting with first argument \(**start**\) till second \(**stop**\) non-included.
* If argument omitted - by default it is either start or end contextually.
* Optional third argument **step **- step.

Examples:

```py
>>> some_string[0:4]
'Some'

>>> some_string[5:10]
'funny'

>>> some_string[0:-1]
'Some funny string'

>>> some_string[:]
'Some funny string!'
```

And some more examples:

```py
>>> some_string[:10:2]
'Sm un'

>>> some_string[::3]
'Seuytn'

>>> some_string[::-1]
'!gnirts ynnuf emoS'
```

##### Splitting/joining {#Splitting/joining}

```py
some_string = "sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef"
print(some_string.split(" "))
print(some_string.split())
print(some_string.split("n"))
print(some_string.split("!"))
print(some_string.split("ZZZZ"))
```

Output:

```
['sdfsdfsdf', '!', '', '', '', '', 'sdfsdff', '\t', '\n', 'wdfwefwefwef', 'wefwef']
['sdfsdfsdf', '!', 'sdfsdff', 'wdfwefwefwef', 'wefwef']
['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']
['sdfsdfsdf ', '     sdfsdff \t \n wdfwefwefwef wefwef']
['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']
```

Joining:

```py
>>> "---".join(["First", "Second", "Third"])
First---Second---Third

>>> ",".join(some_string.split()
sdfsdfsdf,!,sdfsdff,wdfwefwefwef,wefwef
```

### Concatenation {#Concatenation}

Rare case where string can be merged if they are separated by any number of spaces. Strings must be presented by string object themselves not by variables or function call results

```py
>>> "Hello" " World"
'Hello World'
```

One more example:

```py
some_big_string = "Dear Katerina Matveevna! " \
                  "My soul is flying towards you " \
                  "while I'm lost here in this endless desert..."
print(some_big_string)
```

Output:

```
Dear Katerina Matveevna! My soul is flying towards you while I'm lost here in this endless desert...
```

### Formatting {#Formatting}

> There are two \(old one new\) styles of string formatting in Python. They are very similar when dealing with simple stuff but also have a lot of in-deep presentation and text transformation options

1. `str.format()`
   \(new\) provides a large degree of flexibility and customization.
2. `printf-style`
   \(**%**, old\) - based on C printf style formatting that handles a narrower range of types and is slightly harder to use correctly, but is often faster for the cases it can handle.
3. `f-strings`
   \(Python 3.6, super new!\) - inline formatting allowing to insert variables by names with format similar to`format()`

Examples of all formattings:

```py
print_me = "The World is Mine"
print(  "1. %s" % print_me )         # Old format, %
print(  "2. {}".format(print_me) )   # New format, format()
print( f"3. {print_me}")             # f-format
```

Output:

```
1. The World is Mine
2. The World is Mine
3. The World is Mine
```

#### **% **\(printf-style formatting\) {#%-(printf-style-formatting)}

> `format % values`
>
> `format`is a string,`%`conversion specifications in format are replaced with zero or more elements of`values`.

A conversion specifier contains two or more characters and has the following components, which must occur in this order:

`1`. The '%' character - the start of the specifier.

`2`. Mapping key \(optional\), key name in parentheses \(for example:`(somename)`\).

`3`. Conversion flags \(optional\), which affect the result of some conversion types.

`4`. Minimum field width \(optional\). If specified as an '`*`' \(asterisk\), the actual width is read from the next element of the tuple in values, and the object to convert comes after the minimum field width and optional precision.

`5`. Precision \(optional\), given as a '`.`' \(dot\) followed by the precision. If specified as '`*`' \(an asterisk\), the actual precision is read from the next element of the tuple in values, and the value to convert comes after the precision.

`6`. Length modifier \(optional\).

`7`. Conversion type.

In \[45\]:

```
food
=
"Ceasar salad"
print
(
"For breakfast today is 
%s
"
%
food
)
```

```
For breakfast today is Ceasar salad

```

In \[1\]:

```
food
=
"Pizza Pepperoni and burger"
money
=
130.25
print
(
"For lunch we have: 
%29s
, budget: 
%10.3f
 UAH"
%
(
food
,
money
)
)
```

```
For lunch we have:    Pizza Pepperoni and burger, budget:    130.250 UAH

```

In \[12\]:

```
data
=
{
"food"
:
"Pasta Carbonara"
,
"money"
:
300
}
print
(
"And for dinner:  
%(food)20s
, money to spend: 
%(money)s
"
%
data
)
```

```
And for dinner:       Pasta Carbonara, money to spend: 300

```

#### **{}**/ format\(\) {#{}-/-format()}

It's better to use this for something that requries more complex formatting

> Format strings contain “replacement fields” surrounded by curly braces {}. Anything that is not contained in braces is considered literal text, which is copied unchanged to the output. If you need to include a brace character in the literal text, it can be escaped by doubling: {{ and }}.

In \[46\]:

```
print
(
"Our food today is 
{}
"
.
format
(
food
))
```

```
Our food today is Pizza Pepperoni

```

Several arguments:

In \[47\]:

```
print
(
"Food: '
{}
', money: 
{}
 UAH"
.
format
(
food
,
money
))
```

```
Food: 'Pizza Pepperoni', money: 130.25 UAH

```

It is possible when using new format \(_format\(\)_\) to specify positions:

In \[16\]:

```
print
(
"Food is 
{1}
, money: 
{0}
"
.
format
(
money
,
food
))
```

```
Food is Pizza Pepperoni and burger, money: 130.25

```

It is possible to pass arguments by names:

In \[22\]:

    data
    =
    {
    "money"
    :
    45
    ,
    "food"
    :
    "salad"
    }
    # `**` - means we are passing dict as a sequence of key-value pairs
    print
    (
    "Want 
    {food}
     but $
    {money}
     to spend"
    .
    format
    (
    **
    data
    ))
    # print("Want {food} but ${money} to spend".format(money=45, food="salad"))

```
Want salad but $45 to spend

```

More examples:

In \[26\]:

```
"First thing in the morning is 
{0}
"
.
format
(
"coffee"
)
# References first positional argument
```

Out\[26\]:

```
'First thing in the morning is coffee'
```

In \[51\]:

```
"I'd like a 
{}
 with coffee"
.
format
(
"cookie"
)
# Implicitly references the first positional argument
```

Out\[51\]:

```
"I'd like a cookie with coffee"
```

In \[52\]:

```
"Bring me 
{}
 and 
{}
"
.
format
(
"coffee"
,
"cookie"
)
# Same as "From {0} to {1}"
```

Out\[52\]:

```
'Bring me coffee and cookie'
```

In \[53\]:

```
"Remember my name: 
{name}
"
.
format
(
name
=
"Heisenberg"
)
# References keyword argument 'name'
```

Out\[53\]:

```
'Remember my name: Heisenberg'
```

In \[54\]:

```
data
=
dict
(
do_what
=
"Remember"
,
my_what
=
"name"
,
name
=
"Heisenberg"
)
"
{do_what}
 my 
{my_what}
: 
{name}
"
.
format
(
**
data
)
```

Out\[54\]:

```
'Remember my name: Heisenberg'
```

In \[55\]:

```
"String has this method: 
{0.isalpha}
"
.
format
(
""
)
# 'isalpha' attribute of first positional arg
```

Out\[55\]:

```
'String has this method: 
<
built-in method isalpha of str object at 0x0000000000439AB0
>
'
```

### Differences between formatters: {#Differences-between-formatters:}

| % | {} | Ouput |
| :--- | :--- | :--- |
| `'%s %s' % ('one', 'two')` | `'{} {}'.format('one', 'two')` | `one two` |
| `'%d %d' % (1, 2)` | `'{} {}'.format(1, 2)` | `1 2` |
| --- | `'{1} {0}'.format('one', 'two')` | `two one` |
| `'%10s' % ('test',)` | `'{:>10}'.format('test')` | `test` |
| `'%-10s' % ('test',)` | `'{:10}'.format('test')` | `test` |
| --- | `'{:\_<10}'.format('test')` | `test______` |
| --- | `'{:^10}'.format('test')` | `test` |

| % | {} | Ouput |
| :--- | :--- | :--- |
| `'%.3s' % ('abcdef',)` | `'{:.3}'.format('abcdef')` | `abc` |
| `'%d' % (42,)` | `'{:d}'.format(42)` | `42` |
| `'%06.2f' % (3.141592,)` | `'{:06.2f}'.format(3.14159)` | `003.14` |
| --- | `'{p.type}'.format(p=Plant())` | `tree` |

In last example assuming p is the instance of Plant class defined like:

```
class
Plant
(
object
):
type
=
'tree
```

#### .format\(\) cheatsheet {#.format()-cheatsheet}

| Data | Format | Ouput | Decription |
| :--- | :--- | :--- | :--- |
| `3.1415926` | `{:.2f}` | `3.14` | 2 decimal places |
| `3.1415926` | `{:+.2f}` | `+3.14` | 2 decimal places with sign |
| `2.71828` | `{:.0f}` | `3` | No decimal places |
| `1000000` | `{:,}` | `1,000,000` | Number with comma sep |
| `13` | `{:10d}` | `13` | Right aligned |
| `13` | `{:<10d}` | `13` | Left aligned |
| `13` | `{:^10d}` | `13` | Center aligned |

#### .format\(\) "cheats" {#.format()-"cheats"}

* Show the same string several times

In \[56\]:

```
print
(
'''
{0}
!
{1}
. 
"
{0}
!" 
{1}
. 
"What's gone with that boy, I wonder? You 
{0}
!" 
{1}
. 
'''
.
format
(
'TOM'
,
'No answer'
))
```

```
TOM!
No answer. 
"TOM!" 
No answer. 
"What's gone with that boy, I wonder? You TOM!" No answer. 


```

* Convert Values to different Bases
  * You can use the following letters to convert a number to their bases:
    * **d**
      ecimal, he
      **x**
      ,
      **o**
      ctal,
      **b**
      inary

In \[57\]:

```
print
(
"
{0:d}
 - 
{0:x}
 - 
{0:o}
 - 
{0:b}
 "
.
format
(
21
))
```

```
21 - 15 - 25 - 10101 

```

* Escaping braces:

In \[58\]:

```
print
(
"{{0}} / 
{}
"
.
format
(
"TEST"
)
)
```

```
{0} / TEST

```

#### f-strings formatting {#f-strings-formatting}

New feature appeared in Python 3.6. It is possible to inject local variable right into string \(variable interpolation\)

> Formatted string literals are prefixed with 'f' and are similar to the format strings accepted by str.format\(\). They contain replacement fields surrounded by curly braces. The replacement fields are expressions, which are evaluated at run time, and then formatted using the format\(\) protocol

This feature is described by[PEP 498](https://www.python.org/dev/peps/pep-0498/#specification)

The format is:

```
f
' 
<
text
>
 { 
<
expression
>
<
optional !s, !r, or !a
>
<
optional : format specifier
>
 } 
<
text
>
 ... '
```

In \[10\]:

```
var
=
34.125
print
(
f
'
{var}
'
)
print
(
f
'
{var:012.4}
'
)
print
(
f
'
{var:^10}
'
)
```

```
34.125
000000034.12
  34.125  

```

In case interpolating var is not defined - you'll get regular NameError:

In \[11\]:

```
f
'
{unexistent_var}
'
```

```
---------------------------------------------------------------------------
NameError
                                 Traceback (most recent call last)

<
ipython-input-11-046bddf22923
>
 in 
<
module
>
()
----
>
 1
f'{unexistent_var}'
NameError
: name 'unexistent_var' is not defined
```

Expressions may be evaluated directly inside a string:

In \[20\]:

```
f
'{ 1 + 2 }'
```

Out\[20\]:

```
'3'
```

In \[19\]:

```
f
'{"just another string"}'
'quoted string'
```

Out\[19\]:

```
'quoted string'
```

In \[22\]:

```
d
=
{
"a"
:
100500
}
f
'
{d["a"]}
'
```

Out\[22\]:

```
'100500'
```

In \[1\]:

```
def
foo
(
x
):
return
"Hello! 
%s
"
%
x
f
'{foo("John")}'
```

Out\[1\]:

```
'Hello! John'
```

In \[3\]:

```
value
=
1234
f
'input=
{value:#06x}
'
```

Out\[3\]:

```
'input=0x04d2'
```

In \[4\]:

```
import
datetime
date
=
datetime
.
date
(
2017
,
1
,
1
)
f
'
{date}
 was on a {date:%A}'
```

Out\[4\]:

```
'2017-01-01 was on a Sunday'
```

### Dynamic width {#Dynamic-width}

In \[4\]:

```
import
decimal
width
=
10
precision
=
4
value
=
decimal
.
Decimal
(
'12.34567'
)
f
'result: {value:
{width}
.
{precision}
}'
```

Out\[4\]:

```
'result:      12.35'
```

#### Templates {#Templates}

A bit underrated feature of builtin string module._Template_is very simple template engine.

In \[58\]:

```
from
string
import
Template
s
=
Template
(
'$who likes $what'
)
print
(
s
.
substitute
(
who
=
'Johnny'
,
what
=
'whiskey'
))
d
=
dict
(
who
=
'tim'
)
#Template('Give $who $cookie').substitute(d) 
<
--- will raise ValueError as 'cookie' not in a dictionary
print
(
Template
(
'$who likes $cookies'
)
.
safe_substitute
(
d
))
# proper way
```

```
Johnny likes whiskey
tim likes $cookies
```



