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



