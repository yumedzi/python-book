# Super

`super()`

> This function gives you access to methods in a superclass from the subclass that inherits from it.

<img src="../images/tr_07_00.png">

* Return a proxy/temporary object that allows to call superclass’s methods.
* This is useful for accessing inherited methods that have been overridden in a class. The search order is same as that used by `getattr()` except that the type itself is skipped. 

## Usage of `super()`

But first of all let's check what is bound/unbound method

> Method bound to the object is the function that passes that object as the first argument (instance for instance methods, class for class methods).

```python
a = A()
a.method(x) --> A.method(a, x)  # <-- here a.method is bound method
```

> "bound_method is bound method :)

`super()` will return **bound method** depends from context. So for method like `__new__` (which has class as first argument it will return unbound class method).

In the following example notice that we pass `cls` in `__new__()` but in `__init__` we don't pass `self`. This is because in case of `__init__` this method is bound to `self` instance already.

### Usage of super() with different types of methods

Please notice that we don't pass `cls`/`self` into class/instance methods:


🪄 <mark style="color:red;">Code</mark>:

```python
class A:
    attr = "class attr from A"

    def instance_method(self):
        print("Running method of A")
        return self.attr

    @classmethod
    def class_method(cls):
        return cls.attr

    @staticmethod
    def static_method():
        return "Some static data (from A class)"


class C:
    def instance_method(self):
        return "I AM FROM C"


class B(A, C):
    attr = "class attr from B"
    
    def instance_method(self):
        print("Running instance method in B...")
        #return A.instance_method(self)
        return super().instance_method()   # FROM A (next in MRO)
        # return super(B, self).instance_method()   # FROM A (next in MRO)
        #return super(A, self).instance_method()  # FROM C (after A)

    @classmethod
    def class_method(cls):
        print("Running class method in B...")
        # print(f"!!! {A.class_method()}")
        return super().class_method()

    def __new__(cls):
        print("Running __new__...")
        return super().__new__(cls)

    @staticmethod
    def static_method():  # Super difficult
        print("Running static method...")
        #return super(B, B).static_method()
        return A.static_method()

# Working with class A (original, super-class)
a = A()
a.attr = "Object's own attr (from class A)"
print(a.__dict__)
print(a.instance_method())
print(a.class_method())
# print(A.static_method())
print("--------" * 10)

# Working with class B (child to A and C)
b = B()
print(B.mro())
b.attr = "Object's own attr (from class B)"
print(b.instance_method())
print(b.class_method())
print(b.static_method())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
{'attr': "Object's own attr (from class A)"}
Running method of A
Object's own attr (from class A)
class attr from A
--------------------------------------------------------------------------------
Running __new__...
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [299], in <cell line: 58>()
     55 print("--------" * 10)
     57 # Working with class B (child to A and C)
---> 58 b = B()
     59 print(B.mro())
     60 b.attr = "Object's own attr (from class B)"


Input In [299], in B.__new__(cls)
     38 def __new__(cls):
     39     print("Running __new__...")
---> 40     return super().__new__(cls)


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
### More examples:

#### Base class abstraction

The dict that checks for int/str version of the key if it exists:


🪄 <mark style="color:red;">Code</mark>:

```python
class FlexibleDict(dict):
    def __getitem__(self, key):
        try:
            if key in self:
                pass
            elif str(key) in self:
                key = str(key)
            elif int(key) in self:
                key = int(key)
        except ValueError:
            pass
            
        return dict.__getitem__(self, key)

fd = FlexibleDict()
fd[1] = 100500
print(fd["1"])
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
100500
```
{% endcode %}
The dict with logging around setting a key:


🪄 <mark style="color:red;">Code</mark>:

```python
class VerboseDict(dict):
    def __setitem__(self, key, value):
        print(f'Set: {key} -> {value}')
        super().__setitem__(key, value)
        
vd = VerboseDict(x=1, y=2)
vd["z"] = "!"
vd[1] = 100500
vd
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Set: z -> !
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [301], in <cell line: 7>()
      4         super().__setitem__(key, value)
      6 vd = VerboseDict(x=1, y=2)
----> 7 vd["z"] = "!"
      8 vd[1] = 100500
      9 vd


Input In [301], in VerboseDict.__setitem__(self, key, value)
      2 def __setitem__(self, key, value):
      3     print(f'Set: {key} -> {value}')
----> 4     super().__setitem__(key, value)


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
from collections import defaultdict

class VerboseDict(defaultdict):  # new base class
    def __setitem__(self, key, value):
        print(f'Set: {key} -> {value}')
        super().__setitem__(key, value)  # no change needed

vd = VerboseDict(int, x=1, y=2)
vd["z"] = 3
vd[100] = 100500
vd[5]
vd
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Set: z -> 3
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [302], in <cell line: 9>()
      6         super().__setitem__(key, value)  # no change needed
      8 vd = VerboseDict(int, x=1, y=2)
----> 9 vd["z"] = 3
     10 vd[100] = 100500
     11 vd[5]


Input In [302], in VerboseDict.__setitem__(self, key, value)
      4 def __setitem__(self, key, value):
      5     print(f'Set: {key} -> {value}')
----> 6     super().__setitem__(key, value)


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
#### Extending class, multi-inheritance




🪄 <mark style="color:red;">Code</mark>:

```python
from collections import Counter

class VerboseDict(dict):
    def __setitem__(self, key, value):
        print(f'Set: {key} -> {value}')
        super().__setitem__(key, value)

class VerboseCounter(VerboseDict, Counter):
    pass

# This will use __setitem__ from Counter instead of dict
print(f'MRO for VerboseCounter is: {VerboseCounter.mro()}')
counter = VerboseCounter("boombbbam")
print(counter)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
MRO for VerboseCounter is: [<class '__main__.VerboseCounter'>, <class '__main__.VerboseDict'>, <class 'collections.Counter'>, <class 'dict'>, <class 'object'>]
Set: b -> 1
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [303], in <cell line: 13>()
     11 # This will use __setitem__ from Counter instead of dict
     12 print(f'MRO for VerboseCounter is: {VerboseCounter.mro()}')
---> 13 counter = VerboseCounter("boombbbam")
     14 print(counter)


File /opt/conda/lib/python3.10/collections/__init__.py:577, in Counter.__init__(self, iterable, **kwds)
    566 '''Create a new, empty Counter object.  And if given, count elements
    567 from an input iterable.  Or, initialize the count from another mapping
    568 of elements to their counts.
   (...)
    574 
    575 '''
    576 super().__init__()
--> 577 self.update(iterable, **kwds)


File /opt/conda/lib/python3.10/collections/__init__.py:670, in Counter.update(self, iterable, **kwds)
    668             super().update(iterable)
    669     else:
--> 670         _count_elements(self, iterable)
    671 if kwds:
    672     self.update(kwds)


Input In [303], in VerboseDict.__setitem__(self, key, value)
      4 def __setitem__(self, key, value):
      5     print(f'Set: {key} -> {value}')
----> 6     super().__setitem__(key, value)


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
#### Extending list

> This is an example useful to testing.

But in case you want to overload `__new__` method please remember that it is static method so you need to pass `cls`:


🪄 <mark style="color:red;">Code</mark>:

```python
from collections import UserList

class SuperList(list):
    def __new__(cls, data=None, *args):
        result = super().__new__(cls)
        result.append("START")
        if data:
            result.extend(reversed(data))
        result.append("STOP")
        print("Before __init__:", result)
        return result
    
    def __init__(self, data=None, *args):
        'hiding list.__init__ which is resets the list'
#         if data:
#             self.extend(reversed(data))
#         self.append("STOP")
        pass
    
print(SuperList())
print(SuperList("abcde"))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [304], in <cell line: 20>()
     15 #         if data:
     16 #             self.extend(reversed(data))
     17 #         self.append("STOP")
     18         pass
---> 20 print(SuperList())
     21 print(SuperList("abcde"))


Input In [304], in SuperList.__new__(cls, data, *args)
      4 def __new__(cls, data=None, *args):
----> 5     result = super().__new__(cls)
      6     result.append("START")
      7     if data:


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
There is also bigger example for this with lot of print() calls to see where exactly we are at each moment. Please use it to practice and to dig into this a bit more.

We can clearly see that firstly we call `__new__` and after that `__init__`


🪄 <mark style="color:red;">Code</mark>:

```python
class SuperList(list):
    def __new__(cls, *args, **kwargs):
        print(">>> Use parent's constructor but print this line!")
        original_list = super().__new__(cls, *args, **kwargs)
        print(">>> Original list:", original_list)
        print(id(original_list))
        return original_list
    
    def __init__(self, *args, **kwargs):
        print(">>> Before running old __init__:", self)
        super().__init__(*args, **kwargs)
        print(">>> After running old __init__:", self)
        self.append("last element!")
        
l = SuperList("abcde")
print(type(l))
print("New 'list':", l)
l[0] = 100
del l[1]
l[3:5] = ["AAA", "BBB"]
print("After changes:", l)
print(id(l))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
>>> Use parent's constructor but print this line!
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [305], in <cell line: 15>()
     12         print(">>> After running old __init__:", self)
     13         self.append("last element!")
---> 15 l = SuperList("abcde")
     16 print(type(l))
     17 print("New 'list':", l)


Input In [305], in SuperList.__new__(cls, *args, **kwargs)
      2 def __new__(cls, *args, **kwargs):
      3     print(">>> Use parent's constructor but print this line!")
----> 4     original_list = super().__new__(cls, *args, **kwargs)
      5     print(">>> Original list:", original_list)
      6     print(id(original_list))


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
### `super()` based on another class

As resume - we see that super() uses the MRO of passed class (by default it is the class we are defining method for). That's why if we pass another class directly (like it was in Python 2) it will use MRO of that class:


🪄 <mark style="color:red;">Code</mark>:

```python
class A: 
    def m(self):
        return "A"
    
class B(A):
    def m(self):
        return "B"
    
class C(B):
    def m(self):
        return "C"
    
class D(C):
    def m(self):
        print(f"default super()'s MRO is {self.__class__.mro()}")
        print(f"super().m() -> {super().m()} (we take <m> from <C>)")
        print("~" * 60)
        print(f"B's MRO is {B.mro()}")
        print(f"super(B, self).m() -> {super(B, self).m()} (we take <m> from <A>)")
D().m()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
default super()'s MRO is [<class '__main__.D'>, <class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>]
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [306], in <cell line: 20>()
     18         print(f"B's MRO is {B.mro()}")
     19         print(f"super(B, self).m() -> {super(B, self).m()} (we take <m> from <A>)")
---> 20 D().m()


Input In [306], in D.m(self)
     14 def m(self):
     15     print(f"default super()'s MRO is {self.__class__.mro()}")
---> 16     print(f"super().m() -> {super().m()} (we take <m> from <C>)")
     17     print("~" * 60)
     18     print(f"B's MRO is {B.mro()}")


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
More examples:


🪄 <mark style="color:red;">Code</mark>:

```python
class A1:
    attr = 1
class A2:
    attr = 2
class A3:
    attr = 3

class AResult(A1, A2, A3):    
    def __call__(self):       
        return super().attr   
AResult()()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
()



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

Input In [307], in <cell line: 11>()
      9     def __call__(self):       
     10         return super().attr   
---> 11 AResult()()


Input In [307], in AResult.__call__(self)
      9 def __call__(self):       
---> 10     return super().attr


Input In [250], in super.__init__(self, *args, **kwargs)
      2 def __init__(self, *args, **kwargs):             
      3     print(args)                                  
----> 4     self.start_cls, self.instance = args


ValueError: not enough values to unpack (expected 2, got 0)
```
{% endcode %}
The same as `super()`:


🪄 <mark style="color:red;">Code</mark>:

```python
class AResult(A1, A2, A3):
    def __call__(self):
        return super(self.__class__, self).attr
AResult()()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
(<class '__main__.AResult'>, <__main__.AResult object at 0x7f6dddc8c430>)
Running __getattr__, attr = attr





1
```
{% endcode %}
To start FROM A2:


🪄 <mark style="color:red;">Code</mark>:

```python
class AResult(A1, A2, A3):
    def __call__(self):
        return super(A1, self).attr
AResult()()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
(<class '__main__.A1'>, <__main__.AResult object at 0x7f6ddc52cca0>)
Running __getattr__, attr = attr





2
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
class AResult(A1, A2, A3):
    def __call__(self):
        return super(A2, self).attr
AResult()()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
(<class '__main__.A2'>, <__main__.AResult object at 0x7f6dddd50d30>)
Running __getattr__, attr = attr





3
```
{% endcode %}
### Simple `super(cls, obj)` implementation


```python
class super:                                         
    def __init__(self, *args, **kwargs):             
        print(args)                                  
        self.start_cls, self.instance = args         
                                                     
    def __getattr__(self, attr):                     
        print(f"Running __getattr__, attr = {attr}") 
        start = False                                
        for cls in self.instance.__class__.mro():    
            if not start and cls != self.start_cls:  
                continue                             
            if cls == self.start_cls:                
                start = True                         
                continue                             
            if hasattr(cls, attr):                   
                ret = getattr(cls, attr)             
                if callable(ret):                    
                    return lambda: ret(self.instance)
                return ret                           

```


```python
class A:
    def m(self):                                     
        return "A"
    
class B:
    def m(self):                                     
        return "B"
    
class C:
    def m(self):                                     
        return "C"

class D(A, B, C):                                    
    def m(self):                                     
        return super(B, self).m()                    

print(D.mro())                                       
D().m()
```