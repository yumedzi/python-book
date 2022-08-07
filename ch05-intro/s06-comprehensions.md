# Comprehensions

> Comprehensions are considered as most "Pythonic" way of constructing needed data on-the-fly.


* List comprehension
* Dictionary comprehension
* Set comprehensions
* Generator expression\*

## List comprehension

> Bread and butter of day-to-day Python programming


```python
[x for x in range(0, 10)]
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]</span></div>




```python
[x for x in range(0,10) if x%2 == 0]
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">[0, 2, 4, 6, 8]</span></div>




```python
[(x, y) for x in range(0,10) if x%2 == 0 for y in range(x) if y%2 != 0]
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">[(2, 1),
 (4, 1),
 (4, 3),
 (6, 1),
 (6, 3),
 (6, 5),
 (8, 1),
 (8, 3),
 (8, 5),
 (8, 7)]</span></div>



## Dictionary comprehension

> Useful to create a dictionary with the same (default) value or predefined by some logic


```python
{x: str(x) for x in range(5)}
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">{0: '0', 1: '1', 2: '2', 3: '3', 4: '4'}</span></div>




```python
{x: y for x in range(3) for y in range(3)}
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">{0: 2, 1: 2, 2: 2}</span></div>



## Set comprehension

> Not so widely used but still can be quite helpful. For example if you read lines from the file you can collect unqiue ones.


```python
list_with_duplicated = [1, 1, 2, 3, 2, 1, 4, 2]
print({x for x in list_with_duplicated})
print(set(list_with_duplicated)) # recommended way

print({x for x in list_with_duplicated if x % 2}) # more logical usage
```

<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;">{1, 2, 3, 4}
{1, 2, 3, 4}
{1, 3}</span></div>


## Generator expression

> "Kind of" comprehension but instead of returning sequence as other do, generator expression returns generator object.


```python
(x * x for x in range(10))
```




<div><span style="display:block; white-space: pre-wrap; padding:16px; background-color: #000; color: #e2e2e2; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000; border-radius: 4px;"><generator object <genexpr> at 0x0000023DF7253678></span></div>




```python
for x in (x * x for x in range(10)):
    print(x, end=" ")
```

    0 1 4 9 16 25 36 49 64 81