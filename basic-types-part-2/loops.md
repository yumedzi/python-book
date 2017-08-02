# Loops

In Python we have two main ways of creating loops:

* for
* while

## For

```python
for <target> in <target_iterable>:
    <code>
else:
    <if_break_not_called_code>
```

Inside **code** it is possible to use ```continue``` and ```break```:
* ```break``` statement terminates the loop without executing the ```else``` clause’s code
* ```continue``` statement skips the rest of code's statements and continues with the next item, or with the else clause if there is no next item

Example of usecase of "break/else":

```python

courses = get_subscribed_courses(request.user)  # all courses of this user
for session in task.sessions.all():  # task.sessions - all sessions where this task assigned
    if session.course in courses:  # session belongs to assigned course - task is "valid"
        break
else:
    return redirect(reverse('list_hometasks'))  # redirect to the list of tasks

# Returning rendered page with task:
return render(request, template_name, context)
```


```python
for x in range(1, 10):
    print(x, "\t: ", end="")
    if x in [8, 9, 10]:
        print("<---SKIPPING LINE--->")
        continue # immediately go on next iteration of x
    elif x % 2:
        print("Even number", end="")
    elif x == 12:
        print("BYE BYE!!! (break called!)")
        break # completely go out from for loop
    else:
        print("Odd number", end="")
    print(" ... EOL!") # will not triggered if 8 and 10
else:  # run this block only if no break statement called
    print("No break called -- number 12 was NOT FOUND")
```

Output:

    1 	: Even number ... EOL!
    2 	: Odd number ... EOL!
    3 	: Even number ... EOL!
    4 	: Odd number ... EOL!
    5 	: Even number ... EOL!
    6 	: Odd number ... EOL!
    7 	: Even number ... EOL!
    8 	: <---SKIPPING LINE--->
    9 	: <---SKIPPING LINE--->
    No break called -- number 12 was NOT FOUND
    

## Range function

> `range()` returns iterable object needed for arithmetic progression. It is most often used in `for` loops. The arguments must be plain integers. If the step argument is omitted, it defaults to 1

> `range(start, stop[, step])`

> `range(stop)`


```python
print(list(range(10)))
print(list(range(1, 11)))
print(list(range(0, 30, 5)))
print(list(range(0, 10, 3)))
```
Output:

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    [0, 5, 10, 15, 20, 25]
    [0, 3, 6, 9]
    


```python
print(list(range(0, -10, -1)))
print(list(range(0)))
print(list(range(1, 0)))
```
Output:

    [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
    []
    []
    
Also - from 3.5:

```python
>>> [*range(4)]
[0, 1, 2, 3]

>>> [1, 2, *range(3, 6), 6]
[1, 2, 3, 4, 5, 6]

>>> {*range(4), 1, 2}
{0, 1, 2, 3}
```




    




```python

```




    




```python

```

## Pythonic cycles

Try to avoid the code like the following one:

```python
for i in range(len(food)):
    print(food[i])
```

Instead, use clearer "Pythonic" way:

```python
for piece in food:
    print(piece)
```

## Enumerate

> `enumerate(iterable, start=0)`

> Returns an enumerate object which will yield tuples **index, item** from given iterable (a sequence, an iterator, or some other object which supports iteration)


```python
for index, girl in enumerate(["Olya", "Sveta", "Anna", "Maria"], start=1):
    print("Girl number {} is {}".format(index, girl))
```
Output:

    Girl number 1 is Olya
    Girl number 2 is Sveta
    Girl number 3 is Anna
    Girl number 4 is Maria
    

The following code:
    
```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
list(enumerate(seasons))

list(enumerate(seasons, start=1))
```

is equivalent to:

```python
def enumerate(sequence, start=0):
    n = start
    for elem in sequence:
        yield n, elem
        n += 1
```



## While

```python
while <condition>:
    <if_condition_True_code>
else:
    <if_break_not_called_code>
```

Inside **statements** it is possible to use ```continue``` and ```break```:
* ```break``` statement terminates the loop without executing the ```else``` clause’s code
* ```continue``` statement skips the rest of the code's statements and goes back to testing the condition


```python
while True: 
    n = int(input("Please enter an int: "))
    if n < 0: 
        continue # back to the start 
    elif n == 0: 
        break 
    print("Square is ", n ** 2) 
print("Goodbye")
```

Output:

    Please enter an int: 34
    Square is  1156
    Please enter an int: 11
    Square is  121
    Please enter an int: 0
    Goodbye