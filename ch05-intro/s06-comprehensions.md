# Comprehensions

> Comprehensions are considered as most "Pythonic" way of constructing needed data on-the-fly.


* List comprehension
* Dictionary comprehension
* Set comprehensions
* Generator expression\*

## List comprehension

> Bread and butter of day-to-day Python programming


🪄 _<mark style="color:green;">Code:</mark>_

```python
[x for x in range(0, 10)]```




📟 _<mark style="color:green;">Output:</mark>_

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




🪄 _<mark style="color:green;">Code:</mark>_

```python
[x for x in range(0,10) if x%2 == 0]```




📟 _<mark style="color:green;">Output:</mark>_

    [0, 2, 4, 6, 8]




🪄 _<mark style="color:green;">Code:</mark>_

```python
[(x, y) for x in range(0,10) if x%2 == 0 for y in range(x) if y%2 != 0]```




📟 _<mark style="color:green;">Output:</mark>_

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



## Dictionary comprehension

> Useful to create a dictionary with the same (default) value or predefined by some logic


🪄 _<mark style="color:green;">Code:</mark>_

```python
{x: str(x) for x in range(5)}```




📟 _<mark style="color:green;">Output:</mark>_

    {0: '0', 1: '1', 2: '2', 3: '3', 4: '4'}




🪄 _<mark style="color:green;">Code:</mark>_

```python
{x: y for x in range(3) for y in range(3)}```




📟 _<mark style="color:green;">Output:</mark>_

    {0: 2, 1: 2, 2: 2}



## Set comprehension

> Not so widely used but still can be quite helpful. For example if you read lines from the file you can collect unqiue ones.


```python
list_with_duplicated = [1, 1, 2, 3, 2, 1, 4, 2]
print({x for x in list_with_duplicated})
print(set(list_with_duplicated)) # recommended way

print({x for x in list_with_duplicated if x % 2}) # more logical usage
```

📟 _<mark style="color:green;">Output:</mark>_

    {1, 2, 3, 4}
    {1, 2, 3, 4}
    {1, 3}


## Generator expression

> "Kind of" comprehension but instead of returning sequence as other do, generator expression returns generator object.


🪄 _<mark style="color:green;">Code:</mark>_

```python
(x * x for x in range(10))```




📟 _<mark style="color:green;">Output:</mark>_

    <generator object <genexpr> at 0x0000023DF7253678>




🪄 _<mark style="color:green;">Code:</mark>_

```python
for x in (x * x for x in range(10)):
    print(x, end=" ")```

    0 1 4 9 16 25 36 49 64 81