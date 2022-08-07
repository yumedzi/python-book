# Lists

> List is ordered mutable sequence of ANY objects.

> This means that it is allowed to change it's elements after creation: adding new, changing/removing existing etc.

Ways to create a list:
* ```[]```
* ```list()```
* ```[1, 2, 3, [10, 20], 5]```

### Main methods


🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list = [4, 8, 15, 16, 23, 42]
print(dir(some_list))  # Again all methods
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```
{% endcode %}



Actually beside magical methods (containing \_\_) there are not so much methods left

Worth to note that most methods are not returning anything - they are just directly changing the list itself because it is mutable object.

#### List methods

| Method(s)               |  Description                                                                              |
|-------------------------|-----------------------------------------------------------------------------------------
| ```len(some_list)```       | Return int - length of the list
| ```reverse()```            | Reverse order of elements of the list in place
| ```sort()```               | Sort elements of the list in place
| ```append(x)```            | Add new element ```x``` to the end of the list
| ```extend(iterable)```     | Append elements of iterable to the end of the list
| ```pop()```                | Return and remove the last element from the list
| ```pop(i)```               | Return and remove element by index ```i``` from the list

| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```some_list[i]```      | Return (or assign) element by index ```i``` (int)
| ```some_list[i:j]```    | Return new list - slice from element by index ```i``` till ```j-1```
| ```some_list[i:j:z]```  | Return new list - slice with step ```z```
| ```del some_list[3]```     | Remove element of index ```3``` from list ```some_list```
| ```del some_list[2:4]```   | Remove part (starting from index ```2``` till ```3```) from list ```some_list```
| ```2 in some_list```    | Return True/False - is object ```2```is part of list ```some_list```?
| ```some_list + ["a", "b"]``` | Return new list - a sum of merged lists


| Method(s)               |  Description                                                                              |
|-------------------------|-------------------------------------------------------------------------------------------|
| ```count(x)```    | Return number of object ```x``` found in a list
| ```index(x)```    | Return first index of object ```x``` in list or raise ```ValueError``` exception if not found

Last two we saw in strings as well.


## Examples

Lists are indexable, starting at 0


🪄 _<mark style="color:green;">Code:</mark>_

```python
print(some_list)
print(some_list[0])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
4
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list[2]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
15
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list[-1]
```




📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
42
```
{% endcode %}





🪄 _<mark style="color:green;">Code:</mark>_

```python
print(some_list)
print(len(some_list))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
6
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list.reverse()
print(some_list)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[42, 23, 16, 15, 8, 4]
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
some_list.sort()
print(some_list)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42]
```
{% endcode %}




🪄 _<mark style="color:green;">Code:</mark>_

```python
new_list = some_list + ["a", "b", "c"]
print(new_list)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
[4, 8, 15, 16, 23, 42, 'a', 'b', 'c']
```
{% endcode %}



### Sorting

> Sorting of the list with elements of different types in Python 3 is forbidden (yields an TypeError exception about unsupported `'<'` operation).

```python
>>> new_list 
>>> new_list.sort()
TypeError Traceback (most recent call last)

<ipython-input-9-a8ad78a8eda3> in <module>()
      1 new_list