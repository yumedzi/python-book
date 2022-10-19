# Conditions

## if operator

> Python has one omnipotent logical condition check operator: ```if```.

```python
if <condition>:
    <actions_when_condition_is_True>
elif <another_optional_condition>:
    <actions_when_optional_condition_is_True>
else:
    <actions_when_conditions_are_False>
```


🪄 <mark style="color:red;">Code</mark>:

```python
a = 12
if a > 10: 
    print("a is greater than 10" )
elif a == 3: 
    print("a is 3" )
elif a == 5:
    print("a is 5")
else: 
    print("a is lesser than 3")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
a is greater than 10
```
{% endcode %}
## bool type

> Boolean type is subclass of int. So for Python ```True``` is ```1```, ```False``` is ```0```. 

> Its only instances are False and True 

The built-in function bool() can be used to convert any value to a Boolean, if the value can be interpreted as a truth value 


🪄 <mark style="color:red;">Code</mark>:

```python
True + True
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
2
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
(True + True + True) * (True + True) - False
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
6
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
bool(24), bool("sdsds"), bool(""), bool([])
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
(True, True, False, False)
```
{% endcode %}
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

* `or`
* `and`
* `not`
* `^` (`XOR` - exclusive OR - only if its arguments differ)

| Operation    |  Result                        |
|--------------|--------------------------------|
| ```x or y```       | if ```x``` is false, then ```y```, else ```x```
| ```x and y```      | if ```x``` is false, then ```x```, else ```y```
| ```not x```        | if ```x``` is false, then ```True```, else ```False```


Sometimes it can surprise you. The following example will always print the first quote:


🪄 <mark style="color:red;">Code</mark>:

```python
decision = "not to be"
if decision == "be" or "to be":
    print("Take arms against a sea of troubles!")
else:
    print("You will not see this quote anyway =(")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Take arms against a sea of troubles!
```
{% endcode %}
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



## Structural Pattern Matching

Sometimes it is pain to manage the tree-like structure of `if-elif-elif-elif-else` statements. It is becoming a burden to maintain:

```python
if subject == value1:
    <action_1>
elif subject == value2:
    <action_2>
else:
    <default_action>
```

In Python 3.10 we got a completely new syntax for defining of a match statement and case statements of patterns with associated actions allowing substitute a mess of multiple `elif` conditions with a much clear structure. 

The generic syntax of pattern matching is:

```python
match subject:
    case pattern_1:
        <action_1>
    case <pattern_2>:
        <action_2>
    case _:
        <default_action>
```

Pattern matching will try each pattern until a match to run an action from it or the lastly defined `default` match action. The match is comparing the structure/value of the pattern and a given item. It is possible to substitute exact values in the pattern with variables and use them in a action.

An example:


🪄 <mark style="color:red;">Code</mark>:

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 500 | 501 | 502:  # We can use set-like case pattern
            return "Server Error"
        case _:
            return "Something's wrong with the internet"

print(http_error(500))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Server Error
```
{% endcode %}
We can even assign variables using patterns:


🪄 <mark style="color:red;">Code</mark>:

```python
GOOD_MARKS = [4, 5]

def check_student(student: tuple) -> str:
    match student:
        case (name,):
            return f"No mark for student {name} passed"
        case (name, mark):
            return f"Student {name} has a {'good' if mark in GOOD_MARKS else 'bad'} mark"
        case _:
            return "Incorrect value passed - should be: (NAME: str, MARK:int)"

student1 = "John", 5
print(check_student(student1))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Student John has a good mark
```
{% endcode %}
If we don't specify a second tuple item or `None` instead of object:


🪄 <mark style="color:red;">Code</mark>:

```python
print(check_student(("Steve",)))
print(check_student(None))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
No mark for student Steve passed
Incorrect value passed - should be: (NAME: str, MARK:int)
```
{% endcode %}
