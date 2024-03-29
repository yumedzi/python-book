# Comprehensions

> Comprehensions are considered as most "Pythonic" way of constructing needed data on-the-fly.


* List comprehension
* Dictionary comprehension
* Set comprehensions
* Generator expression\*

## List comprehension

> Bread and butter of day-to-day Python programming


🪄 <mark style="color:red;">Code</mark>:

```python
[x for x in range(0, 10)]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
[x for x in range(0,10) if x%2 == 0]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[0, 2, 4, 6, 8]
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
[(x, y) for x in range(0,10) if x%2 == 0 for y in range(x) if y%2 != 0]
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
[(2, 1),
 (4, 1),
 (4, 3),
 (6, 1),
 (6, 3),
 (6, 5),
 (8, 1),
 (8, 3),
 (8, 5),
 (8, 7)]
```
{% endcode %}
## Dictionary comprehension

> Useful to create a dictionary with the same (default) value or predefined by some logic


🪄 <mark style="color:red;">Code</mark>:

```python
{x: str(x) for x in range(5)}
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{0: '0', 1: '1', 2: '2', 3: '3', 4: '4'}
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
{x: y for x in range(3) for y in range(3)}
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{0: 2, 1: 2, 2: 2}
```
{% endcode %}
## Set comprehension

> Not so widely used but still can be quite helpful. For example if you read lines from the file you can collect unqiue ones.


🪄 <mark style="color:red;">Code</mark>:

```python
list_with_duplicated = [1, 1, 2, 3, 2, 1, 4, 2]
print({x for x in list_with_duplicated})
print(set(list_with_duplicated)) # recommended way

print({x for x in list_with_duplicated if x % 2}) # more logical usage
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{1, 2, 3, 4}
{1, 2, 3, 4}
{1, 3}
```
{% endcode %}
## Generator expression

> "Kind of" comprehension but instead of returning sequence as other do, generator expression returns generator object.


🪄 <mark style="color:red;">Code</mark>:

```python
(x * x for x in range(10))
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<generator object <genexpr> at 0x0000023DF7253678>
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
for x in (x * x for x in range(10)):
    print(x, end=" ")
```

    0 1 4 9 16 25 36 49 64 81