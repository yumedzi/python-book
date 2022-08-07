# Strings

> String is **immutable iterable (sequence)** consists of Unicode characters. For Python it's almost like any other sequence (more like tuple which is immutable version of list). 

String literals are written in a variety of ways:

* Single quotes: `'allows embedded "double" quotes'`
* Double quotes: `"allows embedded 'single' quotes".`
* Triple quoted: `'''Three single quotes''', """Three double quotes"""`


```python
s1 = "Hello, I'm nice little string"
s2 = 'Hello, I\'m nice little string'   # escaping '
print(s1)
print(s2)
```

<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">Hello, I'm nice little string
    Hello, I'm nice little string</pre></div>


Multiline string (matter of syntax, for Python they are all the same):


```python
big_string = """Starting here
Going and going and going...
And again and again 
... a bit bored..
I need to rest...
"""
print(big_string)
```

<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">Starting here
    Going and going and going...
    And again and again 
    ... a bit bored..
    I need to rest...</pre></div>
    


### Main methods of strings


```python
print(dir("some_string")) #Emm... actually all methods...
```

<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']</pre></div>


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


```python
some_string + " and another string"
```




<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">'Some funny string! and another string'</pre></div>




```python
some_string * 3
```




<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">'Some funny string!Some funny string!Some funny string!'</pre></div>



##### Get length


```python
len(some_string)
```




<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">18</pre></div>



##### Cosmetic/styling methods:
* lower, upper, title, capitalize


```python
some_string.lower(), some_string.upper(), some_string.title(), some_string.capitalize()
```




<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">('some funny string!',
     'SOME FUNNY STRING!',
     'Some Funny String!',
     'Some funny string!')</pre></div>



##### Various checking for lower/upper, all digits, all letters. Returns True/False.


```python
print("abcde".islower())
print("ABCDE".isupper())
```

<div><pre style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;">True
    True</pre></div>



```python
"12345".isdigit(), "abc".isalpha(), "abc123".isalnum()
```




    (True, True, True)



##### Nice examples regarding checks:


```python
low_str = "asdasdfhjksdhfjh"
low_str.islower(), low_str.isupper()
```




    (True, False)




```python
almost_digit_str = "12123123 123123"
true_digit_str = "12312387877987987"
almost_digit_str.isdigit(), true_digit_str.isdigit()
```




    (False, True)




```python
phone_num = "066-749-99-99"
name = "Johnny"  
name_with_spaces = name + " Walker" # Note that whitespaces are not alpha!
phone_num.isalpha(), name.isalpha(), name_with_spaces.isalpha()
```




    (False, True, False)



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


```python
METHODS = "isdecimal", "isdigit", "isnumeric"
TEST_STRINGS = '123', '1₂34⁵', '½¾⅚', '一二三'

for str_ in TEST_STRINGS:
    for method in METHODS:
        method_str = f'{repr(str_)}.{method}()'
        print(f'{method_str:23} 🡒 {eval(method_str)}')
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


##### Checking for space-containing strings
* To check for all-spaces string - use ```.isspace()```


```python
"    ".isspace(), "  \t \n  \r\n".isspace()
```




    (True, True)



* A bit hackish way to check for alphabeticals with spaces - via using ```.replace()```


```python
"Hello World".replace(" ", "").isalpha()
```




    True



##### Stripping - removing whitespaces
* ```.strip()``` - remove from the beginning and from the end both
* ```.rstrip()``` - remove only from the end
* ```.lstrip()``` - remove only from the beginning


```python
whitespaces_str = "  Some text goes and goes...  "
print("Initial string:   >>>" + whitespaces_str + "<<<")
print("Stripped string: >>>" + whitespaces_str.strip() + "<<<")
print("R-stripped string: >>>" + whitespaces_str.rstrip() + "<<<")
print("L-stripped string: >>>" + whitespaces_str.lstrip() + "<<<")
```

    Initial string:   >>>  Some text goes and goes...  <<<
    Stripped string: >>>Some text goes and goes...<<<
    R-stripped string: >>>  Some text goes and goes...<<<
    L-stripped string: >>>Some text goes and goes...  <<<


##### Get character by index (it's possible because string is sequence)

Indexing starts from 0. Negative indexing means counting from the end so -1 is the last item.


```python
some_string, some_string[0], some_string[3], some_string[-1]
```




    ('Some funny string!', 'S', 'e', '!')



##### Slicing
```some_str[start:stop[:step]]``` (again sequence-like syntax) - getting part of sequence. 

* Returns items with indexes starting with first argument (**start**) till second (**stop**) non-included. 
* If argument omitted - by default it is either start or end contextually. 
* Optional third argument **step** - step.


```python
some_string[0:4], some_string[5:10], some_string[0:-1], some_string[:]
```




    ('Some', 'funny', 'Some funny string', 'Some funny string!')




```python
some_string[:10:2], some_string[::3], some_string[::-1]
```




    ('Sm un', 'Seuytn', '!gnirts ynnuf emoS')



##### Splitting/joining


```python
some_string = "sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef"
print(some_string.split(" "))
print(some_string.split())
print(some_string.split("n"))
print(some_string.split("!"))
print(some_string.split("ZZZZ"))
```

    ['sdfsdfsdf', '!', '', '', '', '', 'sdfsdff', '\t', '\n', 'wdfwefwefwef', 'wefwef']
    ['sdfsdfsdf', '!', 'sdfsdff', 'wdfwefwefwef', 'wefwef']
    ['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']
    ['sdfsdfsdf ', '     sdfsdff \t \n wdfwefwefwef wefwef']
    ['sdfsdfsdf !     sdfsdff \t \n wdfwefwefwef wefwef']



```python
print("---".join(["First", "Second", "Third"]))
print(",".join(some_string.split()))  
```

    First---Second---Third
    sdfsdfsdf,!,sdfsdff,wdfwefwefwef,wefwef


### Concatenation

Rare case where string can be merged if they are separated by any number of spaces. Strings must be presented by string object themselves not by variables or function call results


```python
"Hello" " World"
```




    'Hello World'




```python
some_big_string = "Dear Katerina Matveevna! " \
                  "My soul is flying towards you " \
                  "while I'm lost here in this endless desert..."
print(some_big_string)
```

    Dear Katerina Matveevna! My soul is flying towards you while I'm lost here in this endless desert...



```python
some_big_string = ("Dear Katerina Matveevna! " 
                   "My soul is flying towards you " 
                   "while I'm lost here in this endless desert...")
print(some_big_string)
```

    Dear Katerina Matveevna! My soul is flying towards you while I'm lost here in this endless desert...


### Unicode

#### ASCII

Previously characters used in text data were limited by encoding standard called [ASCII](https://en.wikipedia.org/wiki/ASCII) (American Standard Code for Information Interchange). The key point was "American" so all non-latin characters were missing in that table. 

ASCII basics were simple - single byte of data (8 bits) were used. The first 7 bits were used to code the identifier of the character so totally ASCII had 128 characters (`2^7`). This was done because at that time they though that 128 characters is enough and the last bit was used either for error checking or enabling italics or was set to plain `0`.

Anyway, 128 ASCII characters were: `26` uppercase letters, `26` lowercase letters, `10` digits, punctuation symbols, some spacing characters, and some nonprintable control codes like `\n` (line feed), `\r` (carriage return), `\a` (bell), `\b` (backspace) etc:


```python
import string
print(len(string.ascii_letters) + len(string.digits) + len(string.punctuation) + len(string.whitespace))
```

    100


In Python we can get ASCII "index" of the character with builtin function `ord` and get the character by that index with function `chr`.


```python
print(chr(65))
print(ord("A"))
```

    A
    65


Please note that in fact these functions work with Unicode table (that we will cover in a minute) but Unicode table begins with ASCII and extends it.

We can get all 128 characters of ASCII:


```python
print("ASCII:\n", ''.join(chr(x) for x in range(128)))
```

    ASCII:
      	
     !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~


So, ASCII is great we can't write neither cyrillic texts like `ґуґл з'їв яйко-сподівайко` nor swedish like `Surströmming` with it. The reason is simple - this table just doesn't have needed codepoints for non-latin characters.

That's why at some point other encodings (tables of codepoints) used all 8 bits were created:
* latin-1, windows-1252
    * These cover all main European languages
* windows-1251, koi8
    * These cover most cyrillic languages

To encode Python's string into some endocing the string method `encode(coding)` is used:


```python
print("Surströmming".encode("latin-1"))
# print("Surströmming".encode("windows-1251")) # WON"T WORK
print("ґуґл з'їв яйко-сподівайко".encode("windows-1251"))
#print("ґуґл з'їв яйко-сподівайко".encode("latin-1")) # WON'T WORK
```

    b'Surstr\xf6mming'
    b"\xb4\xf3\xb4\xeb \xe7'\xbf\xe2 \xff\xe9\xea\xee-\xf1\xef\xee\xe4\xb3\xe2\xe0\xe9\xea\xee"