## Regular expressions

> Regular expressions are special universal language for defining text parsing rules. It is widely used for matching parts of the text, finding some information etc.

It is very complex subject to cover so we are going to just look at basic concepts.

More information: https://docs.python.org/3/library/re.html

Regular expression consists of two parts (examples: `a+`, `[a-z]*`, `.*` ):
* **character group** (examples: `a`, `[a-z]`, `\w`, `[\w\d\S]`, `[^a-z]`, `.` )
    * symbol or group of symbol that should be mathched
* **quantifier** (examples: `*`, `+`, `?`, `{5}`, `{1,3}` )
    * specification of how many of previous characters should be matched

Email regexp pattern example

> `[\w\.\+\-]+@[a-z0-9\-]+(\.[a-z0-9\-]+)*`

<img src="../images/tr_02_02.png" />


##### Character group

Examples:
* **.** - one any character
* **a** - just character "a"
* **[abc]** - one from three characters
* **[a-z]** - one from all lowercased charactes
* **[^abc]** - anything except "a", "b" or "c"
* **\w** - any alphabetical character (`[a-zA-Z0-9_]`), (**\W** - everything except alphabeticals)
* **\d** - any digit (`[0-9]`) (**\D** - anything except digits)
* **\s** - any whitespace (**\S** - anything except whitespaces)

#####  Quantifier

> Number of occurences
 
Examples:
* **\*** - any number (0 or any number) of times
* **+** - any positive number (1 or more) of times
* **?** - 1 or 0 times
* **{n1}** - exactly n1 times
* **{n1,n2}** -from n1 to n2 times

### Regexp cheat sheet

* Anchors
* Character classes
* Quantifiers
* Groups and Ranges

#### Anchors

> To mark some part of the text

| Anchor | Description |
|-------------------|-----------|
| `^` | Start of string, or start of line in multi-line pattern
| `$` | End of string, or end of line in multi-line pattern
| `\b` | Word boundary |


#### Character classes

> To describe target characters to match/search

| Character class | Description |
|-------------------|-----------|
| `.`  | Any character except new line (`\n`)
| `\s` | White space
| `\S` | Not white space
| `\d` | Digit (`[0-9]`)
| `\D` | Not digit
| `\w` | Word (`[a-zA-Z0-9_]`)
| `\W` | Not word

#### Quantifiers

> To specify a number of target character class occurence


| Quantifier | Description |
|-------------------|-----------|
| `*`    | `0` or more (`{0,}`)
| `+`    | `1` or more (`{1,}`)
| `?`    | `0` or `1` (`{0, 1}`)
| `{5}`  | Exactly `5`
| `{3,}` | `3` or more
| `{3,5}`| `3`, `4` or `5`

#### Groups and Ranges

> To set custom characters range or list 

| Group/range | Description |
|-------------------|-----------|
| `(a\|b)`      | `a` or `b`
| `[abc]`      | `a` or `b` or `c`
| `[^abc]`     | Not (`a` or `b` or `c`)
| `[a-z]`      | Lower case letter from `a` to `z` (all lowercases)
| `[A-Z]`      | Upper case letter from `A` to `Z` (all uppercases)
| `[0-9]`      | Digit from `0` to `9`

| Group/range | Description |
|-------------------|-----------|
| `(…)`        | Numbered capturing **Group** (starting from `1`)
| `(?:…)`      | Non-capturing **Group**  (usually used for grouping in regexp)
| `(?P<group_name>:…)`      | Named capturing **Group** with name: `"group_name"`
| `\n`         | Group number `n`

### Examples of patterns

* `.at` matches any three-character string ending with "at", including "hat", "cat", and "bat".
* `[hc]at` matches "hat" and "cat".
* `[^b]at` matches all strings matched by .at except "bat".
* `[^hc]at` matches all strings matched by .at other than "hat" and "cat".
* `^[hc]at` matches "hat" and "cat", but only at the beginning of the string or line.
* `[hc]at$` matches "hat" and "cat", but only at the end of the string or line.
* `\[.\]` matches any single character surrounded by "[" and "]" since the brackets are escaped, for example: "[a]" and "[b]".
* `s.*` matches s followed by zero or more characters, for example: "s" and "saw" and "seed".

* `^\d+$` - positive integer
* `^-\d+$` - negative integer
* `^\+?[\d\s]+(?:\(\d{3}\))?[\d\s-]{4,}$` - phone
* `^(?:19|20)\d{2}$` -  year 1900-2099
* `^[\w\d_\.]{4,}$` - username
* `^[\w.']{2,}(\s[\w.']{2,})+$` - personal name
* `^.{6,}$` - password 6 chars min
* `^.{6,}$|^$` - password or empty string
* `^([a-z][a-z0-9-]+\.)+([a-z]{2,6})$` - domain name
* `^[_]*([a-z0-9]+(\.|_*)?)+@([a-z][a-z0-9-]+\.)+[a-z]{2,6}$` - email 

### Regex Python API

Module `re` has all regexp-related methods:




🪄 _<mark style="color:green;">Code:</mark>_

```python
import re 
print(dir(re))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['A', 'ASCII', 'DEBUG', 'DOTALL', 'I', 'IGNORECASE', 'L', 'LOCALE', 'M', 'MULTILINE', 'Match', 'Pattern', 'RegexFlag', 'S', 'Scanner', 'T', 'TEMPLATE', 'U', 'UNICODE', 'VERBOSE', 'X', '_MAXCACHE', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '__version__', '_cache', '_compile', '_compile_repl', '_expand', '_locale', '_pickle', '_special_chars_map', '_subx', 'compile', 'copyreg', 'enum', 'error', 'escape', 'findall', 'finditer', 'fullmatch', 'functools', 'match', 'purge', 'search', 'split', 'sre_compile', 'sre_parse', 'sub', 'subn', 'template']
```
{% endcode %}

> Pattern is one or more regular expressions describing structure if the text that is needed to be parsed.
>
> Patterns in Python are defined as raw string like: `r"\d+[abc]{2:3}"`. By doing this we can use **\\** for regular expressions without escaping.


An example that illustrates raw strings:


🪄 _<mark style="color:green;">Code:</mark>_

```python
print("Printing string with <\n> and <\t\t> as special characters")
print(r"Printing RAW string with <\n> and <\t\t> as special characters")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Printing string with <
```
{% endcode %}
    > and <		> as special characters
    Printing RAW string with <\n> and <\t\t> as special characters


Module `re` can compile regex pattern making it's repeated usage faster.

Also it is worth to understand the difference between `match` and `search` methods:
 * `match` will try to match string with given pattern from the beginning of the string.
 * `search` will try to find the part of the text to match the given pattern. 
 
That's why in most cases when we are looking for some text the usage `search` is preferred.

Main `re` methods:

* ```compile(pattern)```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Compile pattern to optimize it's future usages in regexes
```
{% endcode %}

* ```match(pattern, text)```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Determine if the RE matches at the beginning of the string.
```
{% endcode %}

* ```search(pattern, text)```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Scan through a string, looking for any location where this RE matches.
```
{% endcode %}

* ```findall(pattern, text)```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Find all substrings where the RE matches, and returns them as a list.
```
{% endcode %}

* ```finditer(pattern, text)```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Find all substrings where the RE matches, and returns them as an iterator.
```
{% endcode %}

#### Groups
> Needed to refer to parts of matched text to obtain needed information from it

* `(...)` - creates numbered group (starting from `1`)
* `(?P<gr_name>...)` - creates named group ("gr_name" in example)
* `(?:...)` - creates unnamed group (usually used for grouping in regexp)

### Match object

If `re.match` or `re.search` do not match the pattern - they will return `None` object.

If they successfully match the pattern - they will return special `re.Match` object that has information about found groups, positions of matched text etc. 

**Match object** has the following methods:
* ```groups()```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Return tuple with all matched groups
```
{% endcode %}

* ```group()```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Return the string matched by the RE
```
{% endcode %}

* ```start()```, ```end()```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Return the starting/ending position of the match
```
{% endcode %}

* ```span()```
📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
* Return a tuple containing the (start, end) positions of the match
```
{% endcode %}
An example of using groups and match object:


🪄 _<mark style="color:green;">Code:</mark>_

```python
import re 
text = """sdfsdfsdf
Foo bar 12x Foo asd  34 sdsdfsdf"""

#m = re.search(r"(?:Foo )?bar\s*(\d+)!", "foobar10A")
m = re.search(r".*(?:Foo )?\b(?P<bar>\w{3})\s*\b(\d+)\b[^x]", text)
if m:
    print( m )    
    print( m.groups() )
    print(m.group() )
    print( m.group(2) )
    print( m.group("bar") )
    print(text[22:34])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
<re.Match object; span=(10, 34), match='Foo bar 12x Foo asd  34 '>
```
{% endcode %}
    ('asd', '34')
    Foo bar 12x Foo asd  34 
    34
    asd
    Foo asd  34 


An example of re-using the previously found group in the regexp. Here we try to find the username and password for the main account (which is defined by `main_user` config option):

> NOTE: we use `re.S` (singleline) flag to make `.` to match any characters including `\n` too.


🪄 _<mark style="color:green;">Code:</mark>_

```python
config = """
main_user: user02

credential user01:U1_#$%^$#jbvsd123
credential user02:U2_^&%^$^sdghjf23
credential user03:U3_&%^GHFHGV2235H
"""

re.search(r"main_user: (\w+).*credential\s+\1:([^\n]*)", config, re.S).groups()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('user02', 'U2_^&%^$^sdghjf23')
```
{% endcode %}

### Multiple matching

If we want to find all occurence of the text matching the given pattern - we should use `re.findall`

```python
re.findall(pattern, string)
```

> Return a list of all non-overlapping matches in the string.
>
> If one or more capturing groups are present in the pattern, return
a list of groups; this will be a list of tuples if the pattern
has more than one group.


🪄 _<mark style="color:green;">Code:</mark>_

```python
text = """user: cmonet324@salon_paris.com
account: ADCORP\Claude.Monet
===========
user: Elizabeth2@windsor.com
account: WINDSOR\Elizabeth.II
===========
user: b.allen@starlabs.com
account: ADCORP\Barry.Allen
"""

pattern = r"""user: ([\w\d@\.]+)
account: \w+\\(\w+)\.?(\w*)?"""

print(f"Result of re.findall: {re.findall(pattern, text)}")

for email, first_name, second_name in re.findall(pattern, text):
    print(f"User <{email}>: {first_name} {second_name}")
    
for m in re.finditer(pattern, text):
    email, first_name, second_name = m.groups()
    print(f"User <{email}>: {first_name} {second_name}")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Result of re.findall: [('cmonet324@salon_paris.com', 'Claude', 'Monet'), ('Elizabeth2@windsor.com', 'Elizabeth', 'II'), ('b.allen@starlabs.com', 'Barry', 'Allen')]
```
{% endcode %}
    User <cmonet324@salon_paris.com>: Claude Monet
    User <Elizabeth2@windsor.com>: Elizabeth II
    User <b.allen@starlabs.com>: Barry Allen
    User <cmonet324@salon_paris.com>: Claude Monet
    User <Elizabeth2@windsor.com>: Elizabeth II
    User <b.allen@starlabs.com>: Barry Allen



🪄 _<mark style="color:green;">Code:</mark>_

```python
pattern
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'user: ([\\w\\d@\\._]+)\naccount: \\w+\\\\(\\w+)\\.?(\\w*)?'
```
{% endcode %}

* string `user: `
* text containing words, digits, `@`, dots and `_` - capturing as group `#1`
* string `\naccount: ` followed by a string containing words ending with `\`
* two capturing groups (`#2` and optional `#3`) for texts containing words only separated by optional (because of `?` quantifier) backslash

<img src="../images/tr_02_03.png" />

### Flags

> Flag is optional argument for all main `re` methods. It changes how RE engine works:

| Regex Flag  | Description |
|-------------|--------------|
| `re.M` |	**M**ulti line. Causes `^` and `$` to match the begin/end of each line (not only begin/end of string)
| `re.I` |	Case **i**sensitive
| `re.S` | 	**S**ingle line. Dot matches newline characters 
| `re.X` |  E**x**tended. Spaces and text after a `#` in the pattern are ignored

### Greediness

> 'Greedy' means match longest possible string.
>
> 'Lazy' means match shortest possible string.


By default quantifiers "\*" and "+" are greedy - this means that regexp will try to match as much text as possible.
Let's check the following example where we can see that regexp will match too much (where we wanted to parse out the contents of the tag "span"):



🪄 _<mark style="color:green;">Code:</mark>_

```python
html = "<span>text1</span> and <span>text2</span> and <span>text3</span>"

re.findall(r"<span>(.*)</span>", html)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['text1</span> and <span>text2</span> and <span>text3']
```
{% endcode %}
To make these quantifiers (`*` and `+`) lazy (non-greedy) to much as few as possible we can add `?` to them.
Now the example from above correctly returns the contents of all `<span>` tags:


🪄 _<mark style="color:green;">Code:</mark>_

```python
html = "<span>text1</span> and <span>text2</span> and <span>text3</span>"

re.findall(r"<span>(.*?)</span>", html)
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['text1', 'text2', 'text
```
{% endcode %}
3']