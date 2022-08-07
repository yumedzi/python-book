#### Unicode 

As we could see, the main problem in those 8bit encoding is their limitation and incompatiblity with each other. 

Also what about chinese/japanese hieroglyphs (few thoundands of each) or emojis like ☕, ⚜, 🌠 or ⛄?

That's why Unicode was born!

> [Unicode](https://en.wikipedia.org/wiki/Unicode) is an international standard to encode the characters of all the world’s languages, plus symbols from mathematics and other fields.

> Unicode provides a unique number for every character, no matter what the platform, nomatter what the program, no matter what the language.

Unicode is a registry for all known characters. Current Unicode 13.0 (March 2020) contains `143,924` characters:

* `143,696` graphic characters
* `163` format characters
* `65` control characters
    
Unicode covering `154` modern and historic scripts, as well as multiple symbol sets and emoji.

Each Unicode symbol has unique name and codepoint (it's number). Codepoint included a plane (set of characters) and the number of this character in that plain.

Some examples:

```python
0061    'a'; LATIN SMALL LETTER A
...
007B    '{'; LEFT CURLY BRACKET
...
265F    '♟'; BLACK CHESS PAWN
...
2615   '☕'; HOT BEVERAGE
...
0419   'ґ'; CYRILLIC CAPITAL LETTER GHE WITH UPTURN
```

Let's check our `ґ` character:

|Parameter|Values|
|-----|-----|
|Value       | ґ
|Name        | Cyrillic Small Letter Ghe with Upturn |
|Codepoint   | 0491 |
| In Python  | `'\u0491'`
| Link       | [https://unicode-table.com/en/0491/](https://unicode-table.com/en/0491/)


or ☕:

|Parameter|Values|
|-----|-----|
|Value       | ☕
|Name        | Hot Beverage |
|Codepoint   | 2615 |
| In Python  | `'\u2615'`
| Link       | [https://unicode-table.com/en/2615/](https://unicode-table.com/en/2615/)


String in Python 3 is a sequence of code points.


🪄 _<mark style="color:green;">Code:</mark>_

```python
s = 'ґуґл 💝 ☕'
s.upper()
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'ҐУҐЛ 💝 ☕'
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
s[0]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'ґ'
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
'\u0491 and \u2615'
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'ґ and ☕'
```
{% endcode %}




Via builtin module `unicodedata` it is possible to get the standardized name of Unicode character or resolve that name into a character:


🪄 _<mark style="color:green;">Code:</mark>_

```python
import unicodedata
print(unicodedata.name("ґ"))
print(unicodedata.name("☕"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
CYRILLIC SMALL LETTER GHE WITH UPTURN
HOT BEVERAGE
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
cap_char = unicodedata.name("ґ").replace("SMALL", "CAPITAL")
print(cap_char)
print(unicodedata.lookup(cap_char))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
CYRILLIC CAPITAL LETTER GHE WITH UPTURN
Ґ
```
{% endcode %}



### Encoding and Decoding

So, let's summary previous section:
* `Unicode` is the registry of all known characters
* Unicode character has a codepoint and generalized name
* Unicode string is a sequence of code points, which are numbers from 0 through 0x10FFFF (1,114,111 decimal). 

Unicode string needs to be represented in memory as a set of code units, and code units are then mapped to 8-bit bytes. The rules for translating a Unicode string into a sequence of bytes are called a *character encoding*, or just an *encoding*. The opposite procedure is called *decoding*.

> Note: In Python 3 "utf8" is the default encoding, so we can skip it in `encode` and `decode` methods.

* encoding (transform Unicode into `bytes`)
    * `'Ґaнок'.encode('utf8')`
* decoding (transform `bytes` into Unicode)
    * `b'\xd2\x90\xd0\xb0\xd0\xbd\xd0\xbe\xd0\xba'.decode('utf8')`

Encoding:

`str.encode(encoding='utf-8', errors='strict')`

> Encode the string using the codec registered for encoding.

`errors` by default is 'strict' meaning that encoding errors raise a `UnicodeEncodeError`.  Other possible values are `'ignore'`, `'replace'` and `'xmlcharrefreplace'`.


🪄 _<mark style="color:green;">Code:</mark>_

```python
'Ґ'.encode('ascii', 'ignore')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b''
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
'Ґ'.encode('ascii', 'replace')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'?'
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
'Ґ'.encode('ascii', 'xmlcharrefreplace')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'&#1168;'
```
{% endcode %}




Decoding:

`bytes.decode(encoding='utf-8', errors='strict')`

> Decode the bytes using the codec registered for encoding.

`errors` is by default is 'strict' meaning that decoding errors raise a `UnicodeDecodeError`. Other possible values are `'ignore'` and `'replace'`.

### UTF-8

> UTF-8 is dynamicly sized Unicode Transformation Format

[UTF-8](https://en.wikipedia.org/wiki/UTF-8) is one of the best encodings made specifically to cover Unicode characters. 

UTF-8 is the standard text encoding in Python, Linux, osX, modern Windows and Web. 

UTF-8 is dynamic and can use not just 1 byte (8bit) but dynamically from 1 byte to 4 byte:
* `1` byte for ASCII
* `2` bytes for most Latin-derived and Cyrillic languages
* `3` bytes for the rest of the basic multilingual plane
* `4` bytes for Asian languages, symbols and emojis