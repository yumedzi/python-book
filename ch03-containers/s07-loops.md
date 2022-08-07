# Loops


Python has two loops available in syntax:
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

Notes:
* `for` fetches all items from iterable by firstly converting it to iterable by `iter()` then calling `next()` on it. 

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

Here is a monster-kind example which aims to show all usecases of `for` loop. You can use it as a base for your experiments:


```python
for x in range(1, 15):
    print(x, "\t: ", end="")
    if x in [8, 9, 10]:
        print("<---SKIPPING LINE--->")
        continue # immediately go on next iteration of x
    if x % 2:
        print("Even number", end="")
    else:
        print("Odd number", end="")
    if x == 12:
        print("\nBYE BYE!!! (break called!)")
        break # completely go out from for loop
    print(" ... EOL!") # will not triggered if 8 and 10
else:  # run this block only if no break statement called
    print("No break called -- number 12 was NOT FOUND")
```

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>1 	: Even number ... EOL!
    2 	: Odd number ... EOL!
    3 	: Even number ... EOL!
    4 	: Odd number ... EOL!
    5 	: Even number ... EOL!
    6 	: Odd number ... EOL!
    7 	: Even number ... EOL!
    8 	: <---SKIPPING LINE--->
    9 	: <---SKIPPING LINE--->
    10 	: <---SKIPPING LINE--->
    11 	: Even number ... EOL!
    12 	: Odd number
    BYE BYE!!! (break called!)</code></span>


One more example for for-else loop - selection of DB:

```python

default = "master"
slaves = ["slave1", "slave2", "slave3"]
random.shuffle(slaves)

for slave in slaves:
    if self.is_alive(slave):
        selected = slave
        break
else:
    selected = default
```

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

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    [0, 5, 10, 15, 20, 25]
    [0, 3, 6, 9]</code></span>



```python
print(list(range(0, -10, -1)))
print(list(range(0)))
print(list(range(1, 0)))
```

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
    []
    []</code></span>


Also - from 3.5:


```python
[*range(4)]
```




<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[0, 1, 2, 3]</code></span>




```python
[1, 2, *range(3, 6), 6]
```




<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[1, 2, 3, 4, 5, 6]</code></span>




```python
{*range(4), 1, 2}
```




<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>{0, 1, 2, 3}</code></span>



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

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Girl number 1 is Olya
    Girl number 2 is Sveta
    Girl number 3 is Anna
    Girl number 4 is Maria</code></span>


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

<span style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Please enter an int: 12
    Square is  144
    Please enter an int: 25
    Square is  625
    Please enter an int: 0</code></span>
    Goodbye