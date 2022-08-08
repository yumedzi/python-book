# Generators

> Generator is non-exiting function that stores it's state in memory and can return result values many times when called.

> Generator is the result of generator function

Generators function looks like regular function but instead of ```return``` they use ```yield``` which will return provided value and "freeze" generator state. Next time generator is called it will be resumed from the next statement after ```yield```.

After creation of generator we can call it's ```__next__()``` method to get next value (```next()``` for Python2). If no items will be available (function will end) ```StopIteration``` exception will be thrown to indicate this.

So, `function` is a "`generator function`" if it has `yield` statement.

The result of `generator function` is called `generator`.

Generator is specific kind of object that has `__next__` method which returns "next" value until raising `StopIteration` exception meaning that it is the end of data.

Generator is particular case of more generic type - "iterator" which is defined as object with `__next__` and `__iter__` methods.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def sum_range(x, y):
    print("Starting generator...")
    for i in range(x + y):
        yield i
        print("Next iteration!")
    print("Stopping generator...Bye-bye!")

gen = sum_range(2, 2)
print("First __next__:", next(gen))
print("Second __next__:", next(gen))

for x in gen:  # Recommended way of looping
    print("For loop:", x)

try:
    print("__next__ on 'empty':", gen.__next__())
except StopIteration:
    print("Generator is already empty (raised StopIteration)")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Starting generator...
First __next__: 0
Next iteration!
Second __next__: 1
Next iteration!
For loop: 2
Next iteration!
For loop: 3
Next iteration!
Stopping generator...Bye-bye!
Generator is already empty (raised StopIteration)
```
{% endcode %}
## Generator expressions

Very similar to list comprehension. Instead of sqaure brackets `[]` for generator expressions it's needed to use parentheses `()`.

> Important thing to understand - generator is the result of calling generator function or the result of running generator expression


🪄 _<mark style="color:green;">Code:</mark>_

```python
gen = (x for x in range(1,10) if not x % 2) # get generator using generator expression
print(gen)

for i in gen:
    print(i)
gen = (x for x in range(1,10) if not x % 2) # get generator using generator expression

print(list(gen))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
<generator object <genexpr> at 0x7f3e79f23c78>
2
4
6
8
[2, 4, 6, 8]
```
{% endcode %}
🪄 _<mark style="color:green;">Code:</mark>_

```python
def gen_func():
    for x in range(1, 10):
        if not x % 2:
            yield x
gen = gen_func() #  get generator object by using generator function 
print(gen)
for i in gen:
    print(i)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
<generator object gen_func at 0x103dcf518>
2
4
6
8
```
{% endcode %}
