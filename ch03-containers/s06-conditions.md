# Conditions

> Python has one omnipotent logical condition check operator: ```if```.

```python
if <condition>:
    <actions_when_condition_is_True>
elif <another_optional_condition>:
    <actions_when_optional_condition_is_True>
else:
    <actions_when_conditions_are_False>
```


```python
a = 12
if a > 3: 
    print("a is greater than 3" )
elif a == 3: 
    print("a is 3" )
else: 
    print("a is lesser than 3")
```

<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>a is greater than 3</code></pre>


## bool type

> Boolean type is subclass of int. So for Python ```True``` is ```1```, ```False``` is ```0```. 

> Its only instances are False and True 

The built-in function bool() can be used to convert any value to a Boolean, if the value can be interpreted as a truth value 


```python
True + True
```




<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>2</code></pre>




```python
(True + True + True) * (True + True) - False
```




<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>6</code></pre>




```python
bool(24), bool("sdsds"), bool(""), bool([])
```




<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>(True, True, False, False)</code></pre>




## Truth Value Testing

Any object can be tested for truth value, for use in an if or while condition or as operand of the Boolean operations below. The following values are considered `False`:

* None
* False
* zero of any numeric type, for example, `0`, `0.0`, `0j`.
* any empty iterable, for example, `''`, `()`, `[]`, `set()`, `frozenset()`.
* any empty mapping, for example, `{}`.
* instances of user-defined classes, if the class defines a `__bool__()` or `__len__()` method, when that method returns the integer zero or bool value False.

All other values are considered true — so objects of many types are always true.

## Boolean operations

* or
* and
* not

| Operation    |  Result                        |
|--------------|--------------------------------|
| ```x or y```       | if ```x``` is false, then ```y```, else ```x```
| ```x and y```      | if ```x``` is false, then ```x```, else ```y```
| ```not x```        | if ```x``` is false, then ```True```, else ```False```


Sometimes it can surprise you. The following example will always print the first quote:


```python
decision = "not to be"
if decision == "be" or "to be":
    print("Take arms against a sea of troubles!")
else:
    print("You will not see this quote anyway =(")
```

<pre style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Take arms against a sea of troubles!</code></pre>


Because the expression is equivalent to:
```python
(decision == "be") or ("to be")
```

Solution:
```python
decision in ("be", "to be")
```

## Precedence of operations in Python:

The following table summarizes the operator precedence in Python, from lowest precedence (least binding) to highest precedence (most binding). Operators in the same box have the same precedence. Unless the syntax is explicitly given, operators are binary. Operators in the same box group left to right (except for exponentiation, which groups from right to left).


|Operator	|Description  |
|-----------|-------------|
|`lambda`                                        	| Lambda expression
|`- if – else`                                        | Conditional expression
|`or`, `and`, `not x`	                            | **Boolean OR, AND, NOT**
|`in`, `not in`, `is`, `is not`, `<`, `<=`, `>`, `>=`, `!=`, `==` |	**Comparisons, including membership tests and identity tests**
| <code>&#124;</code>, `^`, `&`                                      | Bitwise OR, XOR, AND
|`<<`, `>>`                                         | Shifts
|`+`, `-`                                           | **Addition and subtraction**
|`*`, `@`, `/`, `//`, `%`                           | **Multiplication, matrix multiplication, division, floor division, remainder** 
|`+x`, `-x`, `~x`	                                | Positive, negative, bitwise NOT
|`**`                                               | Exponentiation
|`await x`                                            | Await expression
|`x[index]`, `x[index:index]`, `x(arguments...)`, `x.attribute`                | **Subscription, slicing, call, attribute reference**
|`(expressions...)`, `[expressions...]`, `{key: value...}`, `{expressions...}` | Binding or tuple display, list display, dictionary display, set display