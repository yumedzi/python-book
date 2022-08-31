## Iterator

> Iterator is an object representing a stream of data; this object returns the data one element at a time.

Iterator must support a method called `__next__()` that takes no arguments and always returns the next element of the stream. If there are no more elements in the stream, `__next__()` must raise the StopIteration exception. Iterators don’t have to be finite, though; it’s perfectly reasonable to write an iterator that produces an infinite stream of data.

The built-in `iter()` function takes an arbitrary object and tries to return an iterator that will return the object’s contents or elements, raising TypeError if the object doesn’t support iteration. Several of Python’s built-in data types support iteration, the most common being lists and dictionaries. An object is called iterable if you can get an iterator for it.


### Iterator protocol
 
Iterator is:
* Object with defined `__next__()` (`next()` for Python2), `__iter__()`
    * `__next__()` takes no arguments and always returns the next element of the stream. If there are no more elements in the stream, `__next__()` must raise the `StopIteration` exception
        * iterator can be infinite
    * `__iter__()` return self (to use inside `for` loop which uses `iter()` for it's data)
* Object returned by generator function (the one that uses `yield`)
* Object returned by `iter(<iterable>)`

<center>
<img src="../images/tr_05_02.jpg" style="align: center">
</center>

### Iterator vs generator

> Generator is partial case of iterator.

<center>
<img src="../images/tr_05_03.jpg" style="align: center">
</center>


### Iterator main methods

* `__next__()` gives next value or raises `StopIteration` exception
* `__iter__()` returns iterator itself (used by `for` operator)
 
So, it's exactly how `for` and `iter` works! It just used object's `__iter__()` method. In other case object must support the sequence protocol (the `__getitem__()` method with integer arguments starting at `0`).

The best way to get all elements of iterator - it's to feed it to `list()`


🪄 _<mark style="color:red;">Code</mark><mark style="color:green;"></mark>:_

```python
list(iter([1, 2, "a", None, 10.1]))
```




📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
[1, 2, 'a', None, 10.1]
```
{% endcode %}
🪄 _<mark style="color:red;">Code</mark><mark style="color:green;"></mark>:_

```python
a = [1, 2, 3, 4]
print( "__next__" in a ) # list doesn't have __next__() --> not iterator! just iterable

print( a.__iter__ )
print (a.__iter__().__next__())
a_iter = iter(a)
print( a_iter )
print (a_iter.__next__(), a_iter.__next__(), a_iter.__next__(), a_iter.__next__())
print (a_iter.__next__())
```

📟 _<mark style="color:green;">Output</mark>:_

{% code overflow="wrap" %}
```
False
<method-wrapper '__iter__' of list object at 0x000000000441FC48>
1
<list_iterator object at 0x00000000043AE860>
1 2 3 4



---------------------------------------------------------------------------

StopIteration                             Traceback (most recent call last)

<ipython-input-25-e15c83738056> in <module>()
      7 print( a_iter )
      8 print (a_iter.__next__(), a_iter.__next__(), a_iter.__next__(), a_iter.__next__())
----> 9 print (a_iter.__next__())


StopIteration:
```
{% endcode %}
