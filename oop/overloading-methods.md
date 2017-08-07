# Overloading methods

> When inheriting from some class it is often required to not completely rewrite some method but to add functionality to existing inherited one. To achieve this function `super()` is widely used.

`super()`

* Return a proxy object that delegates method calls to a parent or sibling class of type.
* This is useful for accessing inherited methods that have been overridden in a class. The search order is same as that used by `getattr()` except that the type itself is skipped. 

## Usage of `super()`

But first of all let's check what is bound/unbound method

> Bound method is method that kind-of already has `self` as first argument already.

> `A().bound_method(x)` --> `A.bound_method(A, x)`

> "bound_method is bound method :)

`super()` will return bound method depends from context. So for method like `__new__` (which has class as first argument it will return unbound class method).

In the following example notice that we pass `cls` in `__new__()` but in `__init__` we don't pass `self`. This is because in case of `__init__` this method is bound to `self` instance already.

Please notice that we don't pass `cls`/`self` into class/instance methods:


```python
class A(object):
    attr = "TEST ATTR"
    @classmethod
    def class_method(cls):
        return cls.attr
    def instance_method(self, arg1, arg2):
        return self.attr
    @staticmethod
    def static_method(x):
        return x

class B(A):
    @classmethod
    def class_method(cls):
        return super().class_method()
    def instance_method(self, arg1, arg2):
        return super().instance_method(arg1, arg2)
    def __new__(cls):
        print("Running __new__")
        return super().__new__(cls)
    @staticmethod
    def static_method(x): # Super difficult
        super(B, B).static_method(x)

print(B().instance_method(1,2))
print(B().class_method())
print(B().static_method(22))
```
Output:

    Running __new__
    TEST ATTR
    Running __new__
    TEST ATTR
    Running __new__
    None
    

But in case you want to overload `__new__` method please remember that it is static method so you need to pass `cls`:


```python
class SuperList(list):
    def __new__(cls, data=None, *args):
        result = super().__new__(cls)
        if data:
            result.extend(data)
        result.append("STOP")
        return result
    def __init__(self, *args):
        'hiding list.__init__ which is resets the list'
        pass
    
print(SuperList())
print(SuperList("abcde"))
```
Output:

    ['STOP']
    ['a', 'b', 'c', 'd', 'e', 'STOP']
    

There is also bigger example for this with lot of print() calls to see where exactly we are at each moment. Please use it to practice and to dig into this a bit more.

It is possible to see clearly that firstly `__new__` is called and after that -  `__init__`.

```python
class SuperList(list):
    def __new__(cls, *args, **kwargs):
        print("*** Use parent's constructor but print this line!")
        original_list = super().__new__(cls, *args, **kwargs)
        print("*** Original list:", original_list)
        print(original_list, id(original_list))
        return original_list
    
    def __init__(self, *args, **kwargs):
        print("*** Init a custom list!")
        super().__init__(*args, **kwargs)
        self.append("last element!")
        
l = SuperList(range(10))
print(type(l))
print("New 'list':", l)
l[0] = 100
del l[1]
l[3:5] = ["AAA", "BBB"]
print("After changes:", l)
```
Output:

    *** Use parent's constructor but print this line!
    *** Original list: []
    [] 4370196904
    *** Init a custom list!
    <class '__main__.SuperList'>
    New 'list': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'last element!']
    After changes: [100, 2, 3, 'AAA', 'BBB', 6, 7, 8, 9, 'last element!']
    
