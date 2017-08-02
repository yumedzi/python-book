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

Ultimate Example:

```python
a = 12
if a > 3: 
    print("a is greater than 3" )
elif a == 3: 
    print("a is 3" )
else: 
    print("a is lesser than 3")
```
Output:

    a is greater than 3
    

## bool type

> Boolean type is subclass of int. So for Python ```True``` is ```1```, ```False``` is ```0```. 

> Its only instances are False and True 

The built-in function `bool()` can be used to convert any value to a Boolean, if the value can be interpreted as a truth value 


```python
>>> True + True
2

>>> (True + True + True) * (True + True) - False
6

>>> bool(24), bool("sdsds"), bool(""), bool([])
(True, True, False, False)
```

## Truth Value Testing

Any object can be tested for truth value, for use in an if or while condition or as operand of the Boolean operations below. The following values are considered false:

* `None`
* `False`
* zero of any numeric type, for example, 0, 0.0, 0j.
* any empty sequence, for example, '', (), [].
* any empty mapping, for example, {}.
* instances of user-defined classes, if the class defines a __bool__() or __len__() method, when that method returns the integer zero or bool value False.

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
