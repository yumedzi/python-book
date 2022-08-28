# Strings

> String is **immutable iterable (sequence)** consists of Unicode characters. For Python it's almost like any other sequence (more like tuple which is immutable version of list). 

String literals are written in a variety of ways:

* Single quotes: `'allows embedded "double" quotes'`
* Double quotes: `"allows embedded 'single' quotes".`
* Triple quoted: `'''Three single quotes''', """Three double quotes"""`


🪄 _<mark style="color:green;">Code:</mark>_

```python
s1 = "Hello, I'm nice little string"
s2 = 'Hello, I\'m nice little string'   # escaping '
print(s1)
print(s2)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Hello, I'm nice little string
Hello, I'm nice little string
```
{% endcode %}
Multiline string (matter of syntax, for Python they are all the same):


🪄 _<mark style="color:green;">Code:</mark>_

```python
big_string = """She’s fifteen, sells flowers at the train station.
Sun and berries sweeten the oxygen beyond the mines.
Trains stop for a moment, move further on.
Soldiers go to the East, soldiers go to the West.
                               (c) Serhiy Zhadan
"""
print(big_string)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
She’s fifteen, sells flowers at the train station.
Sun and berries sweeten the oxygen beyond the mines.
Trains stop for a moment, move further on.
Soldiers go to the East, soldiers go to the West.
                               (c) Serhiy Zhadan
```
{% endcode %}
### Main methods of strings


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(dir("some_string")) #Emm... actually all methods...
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```
{% endcode %}
| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| **Cosmetic methods:**|
| ```lower(), upper()```                | Return new string - in lowercase, uppercase
| ```title(), capitalize()```    | Return new string - all words starts with uppercase, with first word in uppercase 
| `center(w)`, `ljust(w)`, `rjust(w)`  | Return new string centered or justified to left/right in a string of length `w`
| `strip()`, `rstrip()`, `lstrip()`     | Return new string with removed whitespaces
| `replace(s, r[, count])`              | Return new string with all sub-strings `s` replaced by string `r`

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| **Checks:**|
| ```s in some_string```           | Return True/False - if sub-string `s` is part of `some_string`
| `islower()`, `isupper()`         | Return True/False - if all character are in lower/upper case
| ```startswith(s), endswith(s)``` | Return True/False - if string starts/ends with a sub-string `s`
| ```isalpha(), isalnum()``` | Return True/False - are all characters: alphabetical, alpha-numerical?
| ```isdecimal(), isdigit(), isnumeric()``` | Return True/False - are all characters: regular digits, digits with super/subscripts or any numeric Unicode character?
| ```isspace()```                       | Return True/False - are all characters whitespaces (`" "`, `"\n"`, `"\t"` etc.) ?
| `isprintable()`                       | Return True/False - if all characters are printable

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| **Searching:** |
| ```count(s)```                        | Return number of sub-string `s` is part of  string                              
| `index(s)`                        | Return index of first sub-string `s` that found in a string or `ValueError`
| `find(s)`                        | Return index of first sub-string `s` that found in a string or `-1`
| ```len(some_string)```           | Return int - length of string

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| **Split, join, obtaining parts of string:**
| ```split(s)```                   | Return list of string parts splitted by delimiter `s` (whitespace by default)
| ```splitlines(s)```                   | Return list of strings splitted by line ending
| ```s.join(str_iterable)```    | Return new string - result of merging all strings from iterable with strings using delimiter `s`
| ```some_string[i]```             | Return new string - one character by index `i`
| ```some_string[n1:n2:step]```    | Return new string - sub-string from `n1` till `n2` (non-inclusive) with step `step`


#### Some examples


```python
some_string = "Some funny string!"
```

##### Adding, multiplying(!) strings 


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string + " and another string"
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'Some funny string! and another string'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string * 3
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'Some funny string!Some funny string!Some funny string!'
```
{% endcode %}
##### Get length


🪄 _<mark style="color:green;">Code:</mark>_

```python
len(some_string)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
18
```
{% endcode %}
##### Cosmetic/styling methods:
* lower, upper, title, capitalize


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string.lower(), some_string.upper(), some_string.title(), some_string.capitalize()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('some funny string!',
 'SOME FUNNY STRING!',
 'Some Funny String!',
 'Some funny string!')
```
{% endcode %}
##### Various checking for lower/upper, all digits, all letters. Returns True/False.


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("abcde".islower())
print("ABCDE".isupper())
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
True
True
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
"12345".isdigit(), "abc".isalpha(), "abc123".isalnum()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(True, True, True)
```
{% endcode %}
##### Nice examples regarding checks:


🪄 _<mark style="color:green;">Code:</mark>_

```python
low_str = "asdasdfhjksdhfjh"
low_str.islower(), low_str.isupper()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(True, False)
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
almost_digit_str = "12123123 123123"
true_digit_str = "12312387877987987"
almost_digit_str.isdigit(), true_digit_str.isdigit()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(False, True)
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
phone_num = "066-749-99-99"
name = "Johnny"  
name_with_spaces = name + " Walker" # Note that whitespaces are not alpha!
phone_num.isalpha(), name.isalpha(), name_with_spaces.isalpha()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(False, True, False)
```
{% endcode %}
### Checks of numeric/digits

It can be difficult to comprehend from the start, so the following table will show difference between three related methods (`isdecimal(), isdigit(), isnumeric()`):

* `isdecimal()`
    * Only decimal digits: `0123456789`

| Test | Result
|-----------------|--------------------
| `isdecimal('123')`           | `True`
| `isdecimal('1₂34⁵')`         | `False`
| `isdecimal('½¾⅚')`           | `False`
| `isdecimal('一二三四五')`     | `False`

* `isdigit()`
    * decimal digits: `0123456789`
    * super- and subscripts

| Test | Result
|-----------------|---------------
| `isdigit('123')`           | `True`
| `isdigit('1₂34⁵')`         | `True`
| `isdigit('½¾⅚')`           | `False`
| `isdigit('一二三四五')`     | `False`

* `isnumeric()`
    * decimal digits: `0123456789`
    * super- and subscripts
    * vulgar fractions
    * numeric Unicode characters from other languages

| Test | Result
|-----------------|--------------------------
| `isnumeric('123')`           | `True`
| `isnumeric('1₂34⁵')`         | `True`
| `isnumeric('½¾⅚')`           | `True`
| `isnumeric('一二三四五')`     | `True`

The playground code to test these methods on those strings:


🪄 _<mark style="color:green;">Code:</mark>_

```python
METHODS = "isdecimal", "isdigit", "isnumeric"
TEST_STRINGS = '123', '1₂34⁵', '½¾⅚', '一二三'

for str_ in TEST_STRINGS:
    for method in METHODS:
        method_str = f'{repr(str_)}.{method}()'
        print(f'{method_str:23} 🡒 {eval(method_str)}')
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'123'.isdecimal()       🡒 True
'123'.isdigit()         🡒 True
'123'.isnumeric()       🡒 True
'1₂34⁵'.isdecimal()     🡒 False
'1₂34⁵'.isdigit()       🡒 True
'1₂34⁵'.isnumeric()     🡒 True
'½¾⅚'.isdecimal()       🡒 False
'½¾⅚'.isdigit()         🡒 False
'½¾⅚'.isnumeric()       🡒 True
'一二三'.isdecimal()       🡒 False
'一二三'.isdigit()         🡒 False
'一二三'.isnumeric()       🡒 True
```
{% endcode %}
##### Checking for space-containing strings
* To check for all-spaces string - use ```.isspace()```


🪄 _<mark style="color:green;">Code:</mark>_

```python
"    ".isspace(), "  \t \n  \r\n".isspace()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
(True, True)
```
{% endcode %}
* A bit hackish way to check for alphabeticals with spaces - via using ```.replace()```


🪄 _<mark style="color:green;">Code:</mark>_

```python
"Hello World".replace(" ", "").isalpha()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
True
```
{% endcode %}
##### Stripping - removing whitespaces
* ```.strip()``` - remove from the beginning and from the end both
* ```.rstrip()``` - remove only from the end
* ```.lstrip()``` - remove only from the beginning


🪄 _<mark style="color:green;">Code:</mark>_

```python
whitespaces_str = "  Some text goes and goes...  "
print("Initial string:   >>>" + whitespaces_str + "<<<")
print("Stripped string: >>>" + whitespaces_str.strip() + "<<<")
print("R-stripped string: >>>" + whitespaces_str.rstrip() + "<<<")
print("L-stripped string: >>>" + whitespaces_str.lstrip() + "<<<")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Initial string:   >>>  Some text goes and goes...  <<<
Stripped string: >>>Some text goes and goes...<<<
R-stripped string: >>>  Some text goes and goes...<<<
L-stripped string: >>>Some text goes and goes...  <<<
```
{% endcode %}
##### Get character by index (it's possible because string is sequence)

Indexing starts from 0. Negative indexing means counting from the end so -1 is the last item.


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string, some_string[0], some_string[3], some_string[-1]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('Some funny string!', 'S', 'e', '!')
```
{% endcode %}
##### Slicing
```some_str[start:stop[:step]]``` (again sequence-like syntax) - getting part of sequence. 

* Returns items with indexes starting with first argument (**start**) till second (**stop**) non-included. 
* If argument omitted - by default it is either start or end contextually. 
* Optional third argument **step** - step.


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string[0:4], some_string[5:10], some_string[0:-1], some_string[:]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('Some', 'funny', 'Some funny string', 'Some funny string!')
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string[:10:2], some_string[::3], some_string[::-1]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('Sm un', 'Seuytn', '!gnirts ynnuf emoS')
```
{% endcode %}
##### Splitting/joining


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_string = "sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef"
print(some_string.split(" "))
print(some_string.split())
print(some_string.split("n"))
print(some_string.split("!"))
print(some_string.split("ZZZZ"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['sdfsdfsdf', '!', '', '', '', '', 'sdfsdff', '\t', '\n', 'wdfwefwefwef', 'wefwef']
['sdfsdfsdf', '!', 'sdfsdff', 'wdfwefwefwef', 'wefwef']
['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']
['sdfsdfsdf ', '     sdfsdff \t \n wdfwefwefwef wefwef']
['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
print("---".join(["First", "Second", "Third"]))
print(",".join(some_string.split()))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
First---Second---Third
sdfsdfsdf,!,sdfsdff,wdfwefwefwef,wefwef
```
{% endcode %}
### Concatenation

Rare case where string can be merged if they are separated by any number of spaces. Strings must be presented by string object themselves not by variables or function call results


🪄 _<mark style="color:green;">Code:</mark>_

```python
"Hello" " World"
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'Hello World'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
some_big_string = "Everything started with music, " \
                  "with scars left by songs " \
                  "heard at fall weddings with other kids my age."
print(some_big_string)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Everything started with music, with scars left by songs heard at fall weddings with other kids my age.
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
some_big_string = ("You will reply today, touching warm letters, "
                   "leafing through them in the dark, confusing vowels with consonants, "
                   "like a typewriter in an old Warsaw office. ")
print(some_big_string)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
You will reply today, touching warm letters, leafing through them in the dark, confusing vowels with consonants, like a typewriter in an old Warsaw office.
```
{% endcode %}
## Unicode

### ASCII

Previously characters used in text data were limited by encoding standard called [ASCII](https://en.wikipedia.org/wiki/ASCII) (American Standard Code for Information Interchange). The key point was "American" so all non-latin characters were missing in that table. 

ASCII basics were simple - single byte of data (8 bits) were used. The first 7 bits were used to code the identifier of the character so totally ASCII had 128 characters (`2^7`). This was done because at that time they though that 128 characters is enough and the last bit was used either for error checking or enabling italics or was set to plain `0`.

Anyway, 128 ASCII characters were: `26` uppercase letters, `26` lowercase letters, `10` digits, punctuation symbols, some spacing characters, and some nonprintable control codes like `\n` (line feed), `\r` (carriage return), `\a` (bell), `\b` (backspace) etc:


🪄 _<mark style="color:green;">Code:</mark>_

```python
import string
print(len(string.ascii_letters) + len(string.digits) + len(string.punctuation) + len(string.whitespace))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
100
```
{% endcode %}
In Python we can get ASCII "index" of the character with builtin function `ord` and get the character by that index with function `chr`.


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(chr(65))
print(ord("A"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
A
65
```
{% endcode %}
Please note that in fact these functions work with Unicode table (that we will cover in a minute) but Unicode table begins with ASCII and extends it.

We can get all 128 characters of ASCII:


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("ASCII:\n", ''.join(chr(x) for x in range(128)))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
ASCII:
  	
 !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
```
{% endcode %}
So, ASCII is great we can't write neither cyrillic texts like `ґуґл з'їв яйко-сподівайко` nor swedish like `Surströmming` with it. The reason is simple - this table just doesn't have needed codepoints for non-latin characters.

That's why at some point other encodings (tables of codepoints) used all 8 bits were created:
* `latin-1`, `windows-1252`
    * These cover all main European languages
* `latin-2`
    * Central or Eastern European
* `windows-1251`, `koi8`
    * These cover most cyrillic languages
* `big5`
    * Traditional Chinese

To encode Python's string into some endocing the string method `encode(coding)` is used:


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("Surströmming".encode("latin_1"))
# print("Surströmming".encode("windows-1251")) # WON"T WORK

print("Piękna jest taka pewność, ale niepewność jest piękniejsza.".encode("latin2"))

print("Ґуґл з'їв яйко-сподівайко".encode("windows-1251"))
#print("Ґуґл з'їв яйко-сподівайко".encode("latin-1")) # WON'T WORK
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Surstr\xf6mming'
b'Pi\xeakna jest taka pewno\xb6\xe6, ale niepewno\xb6\xe6 jest pi\xeakniejsza.'
b"\xa5\xf3\xb4\xeb \xe7'\xbf\xe2 \xff\xe9\xea\xee-\xf1\xef\xee\xe4\xb3\xe2\xe0\xe9\xea\xee"
```
{% endcode %}
