## Regular expressions

> Regular expressions are special universal language for defining text parsing rules. It is widely used for matching parts of the text, finding some information etc.

It is very complex subject to cover so we are going to just look at basic concepts.

More information: https://docs.python.org/3/library/re.html

Regular expression consists of two parts (examples: `a+`, `[a-z]*`, `.*` ):
* **character group** (examples: `a`, `[a-z]`, `\w`, `[\w\d\S]`, `[^a-z]`, `.` )
    * symbol or group of symbol that should be mathched
* **quantificator** (examples: `*`, `+`, `?`, `{5}`, `{1,3}` )
    * specification of how many of previous characters should be matched

Email regexp pattern example

> `[\w\.\+\-]+@[a-z0-9\-]+(\.[a-z0-9\-]+)*`

![](/assets/tr_01_03.png)

##### Character group

Examples:
* **.** - one any character
* **a** - just character "a"
* **[abc]** - one from three characters
* **[a-z]** - one from all lowercased charactes
* **[^abc]** - anything except "a", "b" or "c"
* **\w** - any alphabetical character (**\W** - everything except alphabeticals)
* **\d** - any digit (**\D** - anything expect digits)
* **\s** - any whitespace (**\S** - anything expect whitespace)

#####  Quantificator
> Number of occurences

 
Examples:
* **\*** - any number (0 or any number) of times
* **+** - any positive number (1 or more) of times
* **?** - 1 or 0 times
* **{n1}** - exactly n1 times
* **{n1,n2}** -from n1 to n2 times

Examples of patterns:

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
* `^([a-z][a-z0-9-]+(\.|-*\.))+[a-z]{2,6}$` - domain name
* `^[_]*([a-z0-9]+(\.|_*)?)+@([a-z][a-z0-9-]+(\.|-*\.))+[a-z]{2,6}$` - email 

#### Regular expressions, methods:

> Pattern is one or more regular expressions describing structure if the text that is needed to be parsed.
> Patterns in Python are defined as raw string like: ```r"\d+[abc]{2:3}"```. By doing this we can use **\\** for regular expressions without escaping.


* ```compile(pattern)```
    * Compile pattern to optimize it's future usages in regexes
* ```match(pattern, text)```
    * Determine if the RE matches at the beginning of the string.
* ```search(pattern, text)```
    * Scan through a string, looking for any location where this RE matches.	
* ```findall(pattern, text)```
    Find all substrings where the RE matches, and returns them as a list.	
* ```finditer(pattern, text)```
    * Find all substrings where the RE matches, and returns them as an iterator.


#### Groups
> Needed to refer to parts of matched text to obtain needed information from it

* `()` - creates numbered group
* `(?P<gr_name>[\w\d]+)` - creates named group ("gr_name" in example)
* `(?:World)` - creates unnamed group (usually used for grouping in regexp)


```python
import re 
text = """sdfsdfsdf
Foo bar 12x Foo bar  34 sdsdfsdf"""
#m = re.search(r"(?:Foo )?bar\s*(\d+)!", "foobar10A")
m = re.search(r".*(?:Foo )?\bbar\s*\b(\d+)\b[^x]", text)
if m:
    print( m )    
    print( m.groups() )
    print(m.group() )
    print( m.group(1) )
    print(text[22:34])
```
Output:

    <_sre.SRE_Match object; span=(10, 34), match='Foo bar 12x Foo bar  34 '>
    ('34',)
    Foo bar 12x Foo bar  34 
    34
    Foo bar  34 
    

**Match object** (result of search(), match()) has the following methods:
* ```groups()```
    * Return tuple with all matched groups
* ```group()```
    * Return the string matched by the RE	
* ```start()```, ```end()```
    * Return the starting/ending position of the match	
* ```span()```
    * Return a tuple containing the (start, end) positions of the match



