# Methods

Methods can be:
* instance methods
* class methods
* static methods

## Instance method

By default all methods (except of `__new__` are instance methods).

The method that should be called with the instance as it's first argument. This method is bound to instance so if calling as it's method passing instance is not required. Example:


```python
class Example(object):
    def cool_method(self):
        print("I am instance method, my instance is: %s" % self)
        
ex = Example()
ex.cool_method()
#Example.cool_method(ex)
```
Output:

    I am instance method, my instance is: <__main__.Example object at 0x10469c278>
    

## Class methods

The method with class as the first argument. Useful to run some code without need of creating the instace. 

To mark the method as class method it is required to use builtin decorator `@classmethod`


```python
class Example:
    attr = 5
    @classmethod
    def class_method(cls):
        print("CLS:", cls.attr)
        
    def instance_method(self):
        print("INSTANCE:", self.attr)
        
ex = Example()
ex.attr = 25
ex.class_method()
ex.instance_method()
Example.class_method() # Example.class_method(Example)
```
Output:

    CLS: 5
    INSTANCE: 25
    CLS: 5
    

## Static method

This method doesn't require an to pass instance/class at all.

To mark the method as static method it is required to use builtin decorator `@staticmethod`


```python
class Example:
    @staticmethod
    def cool_method():
        print("I am a static method, I don't have acces to anything :(")
        
ex = Example()
ex.cool_method()
Example.cool_method()
```
Output:

    I am a static method, I don't have acces to anything :(
    I am a static method, I don't have acces to anything :(
    
