#### Unicode 

As we could see, the main problem in those 8bit encoding is their limitation and incompatiblity with each other. 

Also what about chinese/japanese hieroglyphs (few thoundands of each) or emojis like ☕, ⚜, 🌠 or ⛄?

That's why Unicode was born!

> [Unicode](https://en.wikipedia.org/wiki/Unicode) is an international standard to encode the characters of all the world’s languages, plus symbols from mathematics and other fields.

> Unicode provides a unique number for every character, no matter what the platform, nomatter what the program, no matter what the language.

Unicode is a registry for all known characters. Current Unicode 14.0 (September 2021) contains `144,697` characters:

* `144,697` graphic characters
* `163` format characters
* `65` control characters
    
Unicode covering `159` modern and historic scripts, as well as multiple symbol sets and emoji.

Each Unicode symbol has unique name and codepoint (it's number). Codepoint included a plane (set of characters) and the number of this character in that plain.

Some examples:

```python
0061   'a'; LATIN SMALL LETTER A
...
007B   '{'; LEFT CURLY BRACKET
...
265F   '♟'; BLACK CHESS PAWN
...
2615   '☕'; HOT BEVERAGE
...
0419   'ґ'; CYRILLIC CAPITAL LETTER GHE WITH UPTURN
...
0142   'ł'; LATIN SMALL LETTER L WITH STROKE
```

Let's check our `ґ` character:

|Parameter|Values|
|-----|-----|
|Value       | `ґ`
|Name        | Cyrillic Small Letter Ghe with Upturn |
|Codepoint   | 0491 |
| In Python  | `'\u0491'`
| Link       | [https://unicode-table.com/en/0491/](https://unicode-table.com/en/0491/)


or `ł`:

|Parameter|Values|
|-----|-----|
|Value       | `ł`
|Name        | Hot Beverage |
|Codepoint   | 0142 |
| In Python  | `'\u0142'`
| Link       | [https://unicode-table.com/en/0142/](https://unicode-table.com/en/0142/)


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
🪄 _<mark style="color:green;">Code:</mark>_

```python
w = 'Z\u0142oto daj wiedźminowi'
w[1], w[-7]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
('ł', 'ź')
```
{% endcode %}
Via builtin module `unicodedata` it is possible to get the standardized name of Unicode character or resolve that name into a character:


🪄 _<mark style="color:green;">Code:</mark>_

```python
import unicodedata
print(unicodedata.name("ґ"))
print(unicodedata.name("ł"))
print(unicodedata.name("☕"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
CYRILLIC SMALL LETTER GHE WITH UPTURN
LATIN SMALL LETTER L WITH STROKE
HOT BEVERAGE
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
cap_char = unicodedata.name("ł").replace("SMALL", "CAPITAL")
print(cap_char)
print(unicodedata.lookup(cap_char))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
LATIN CAPITAL LETTER L WITH STROKE
Ł
```
{% endcode %}
### Encoding and Decoding

So, let's summary previous section:
* `Unicode` is the registry of all known characters
* Unicode character has a codepoint and generalized name
* Unicode string is a sequence of code points, which are numbers from 0 through 0x10FFFF (1,114,111 decimal). 

So, Unicode is DB with all characters known to human beings. To write them in a file we can use encodings.

Unicode string needs to be represented in memory as a set of code units, and code units are then mapped to 8-bit bytes. The rules for translating a Unicode string into a sequence of bytes are called a *character encoding*, or just an *encoding*. The opposite procedure is called *decoding*.

> Encoding is a mapping from Unicode DB to the exact bytes used to represent characters.

There are lot of different encodings Python supports: [official doc](https://docs.python.org/3.7/library/codecs.html#standard-encodings).

> Note: In Python 3 "utf8" is the default encoding, so we can skip it in `encode` and `decode` methods.


* encoding (transform Unicode into `bytes`)
    * `'Złoto dla tego Wiedźmina, szybko!'.encode('utf8')`
* decoding (transform `bytes` into Unicode)
    * `b'Wied\xc5\xbamin'.decode('utf8')`
    
As we can see characters present in ASCII are shown as text right away, absent characters are shown in a hex form of bytes used to represent them. 

#### Encoding:

`str.encode(encoding='utf-8', errors='strict')`

> Encode the string using the codec registered for encoding.

`errors` by default is 'strict' meaning that encoding errors raise a `UnicodeEncodeError`.  Other possible values are `'ignore'`, `'replace'`, `'xmlcharrefreplace'` and `backslashreplace`.


🪄 _<mark style="color:green;">Code:</mark>_

```python
'Bo w każdym z nas jest Chaos i Ład, Dobro i Zło.'.encode('ascii', 'ignore')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Bo w kadym z nas jest Chaos i ad, Dobro i Zo.'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
'Bo w każdym z nas jest Chaos i Ład, Dobro i Zło.'.encode('ascii', 'replace')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Bo w ka?dym z nas jest Chaos i ?ad, Dobro i Z?o.'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
'Bo w każdym z nas jest Chaos i Ład, Dobro i Zło.'.encode('ascii', 'xmlcharrefreplace')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Bo w ka&#380;dym z nas jest Chaos i &#321;ad, Dobro i Z&#322;o.'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
'Bo w każdym z nas jest Chaos i Ład, Dobro i Zło.'.encode('ascii', 'backslashreplace')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Bo w ka\\u017cdym z nas jest Chaos i \\u0141ad, Dobro i Z\\u0142o.'
```
{% endcode %}
#### Decoding:

`bytes.decode(encoding='utf-8', errors='strict')`

> Decode the bytes using the codec registered for encoding.

`errors` is by default is 'strict' meaning that decoding errors raise a `UnicodeDecodeError`. Other possible values are `'ignore'` and `'replace'`.

### UTF-8

> UTF-8 is dynamicly sized Unicode Transformation Format

[UTF-8](https://en.wikipedia.org/wiki/UTF-8) is one of the best encodings made specifically to cover Unicode characters. It is the standard encoding of Unicode. That's why UTF-8 is the standard text encoding in Python, Linux, osX, modern Windows and Web. 

UTF-8 is dynamic and can use not just 1 byte (8bit) but dynamically from 1 byte to 4 byte:
* `1` byte for ASCII
* `2` bytes for most Latin-derived and Cyrillic languages
* `3` bytes for the rest of the basic multilingual plane
* `4` bytes for Asian languages, symbols and emojis

Few words on a hex format:
* `0x**` - representation of a number
* `\x**` - representation in a string


🪄 _<mark style="color:green;">Code:</mark>_

```python
0x41
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
65
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
"\x41"
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'A'
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
"\x01" # a non printable character
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'\x01'
```
{% endcode %}
Let's check again our popular `ł` character on [Unicode Table](https://unicode-table.com/en/0142/).

We can see that this character can be represented in various Unicode-friendly encodings:

|Encoding 	| hex  |	      dec (bytes) |	dec  |	binary |
|-----------|------|----------------------|------|------------------------
| UTF-8     | `C5 82`| 	  `197 130` |	`50562` |	`11000101 10000010`
| UTF-16BE 	| `01 42`| 	  `1 66`    |	`322`   |	`00000001 01000010`
| UTF-16LE 	| `42 01`| 	`66 1` 	    | `16897`   |	`01000010 00000001`
| UTF-32BE 	| `00 00 01 42` |	`0 0 1 66` |	`322` |	`00000000 00000000 00000001 01000010`
| UTF-32LE 	| `42 01 00 00` |	`66 1 0 0` |	`1107361792` |	`01000010 00000001 00000000 00000000`


Notice that in `UTF8` it is `C5 82` meaning it should be coded as `\xc5\x82`.

Let's check encoded strings with this character to verify the encoded bytes we supposed to find:


🪄 _<mark style="color:green;">Code:</mark>_

```python
'Bo w każdym z nas jest Chaos i Ład, Dobro i Zło.'.encode('utf8')
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'Bo w ka\xc5\xbcdym z nas jest Chaos i \xc5\x81ad, Dobro i Z\xc5\x82o.'
```
{% endcode %}
Here we see that:
* `ż` was encoded with 2 bytes: `\xc5\xbc`
* `Ł` was encoded with 2 bytes: `\xc5\x81`
* `ł` was encoded with 2 bytes: `\xc5\x82`

Ukrainian characters also use 2 bytes symbols:


🪄 _<mark style="color:green;">Code:</mark>_

```python
"Сію-вію, сію-вію конопелечки...".encode("utf8")
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'\xd0\xa1\xd1\x96\xd1\x8e-\xd0\xb2\xd1\x96\xd1\x8e, \xd1\x81\xd1\x96\xd1\x8e-\xd0\xb2\xd1\x96\xd1\x8e \xd0\xba\xd0\xbe\xd0\xbd\xd0\xbe\xd0\xbf\xd0\xb5\xd0\xbb\xd0\xb5\xd1\x87\xd0\xba\xd0\xb8...'
```
{% endcode %}
Japanese katakana (word means "Python" - `paisonu`), as we can each character takes `3` bytes:


🪄 _<mark style="color:green;">Code:</mark>_

```python
python_in_japanese = 'パイソン'

print(python_in_japanese.encode('utf8'))
print(int(len(python_in_japanese.encode('utf8')) / len(python_in_japanese)))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'\xe3\x83\x91\xe3\x82\xa4\xe3\x82\xbd\xe3\x83\xb3'
3
```
{% endcode %}
And lastly, emojis take `3-4` characters:


🪄 _<mark style="color:green;">Code:</mark>_

```python
print('☕'.encode('utf8'))
print('🐍'.encode('utf8'))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
b'\xe2\x98\x95'
b'\xf0\x9f\x90\x8d'
```
{% endcode %}
