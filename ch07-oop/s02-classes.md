## OOP in Python

### Class

Classes created with operator `class`:
 
```python 
class A:
    attr = 10
```
 
When a class definition is entered, a new namespace is created, and used as the local scope — thus, all assignments
to local variables go into this new namespace. In particular, function definitions bind the name of the new function here

Class objects support two kinds of operations: attribute references and instantiation.


```python
class Bus:
    """ Sample Bus class """
    # Class attributes
    buses_count = 0
    people_transferred = 0
    buses = []
 
    # Instance Initializer
    def __init__(self, name="Some Bus", rate=7):
        # instance attribute
        self.name = name
        self.people_transferred = 0
        self.rate = rate
        Bus.buses_count += 1  # self.__class__.buses_count += 1
        Bus.buses.append(self)
 
    # Instance method
    def transfer(self, num=1):
        self.people_transferred += num
        self.__class__.people_transferred += num
 
    def info(self): # change to __str__
        data = dict(
            name=self.name, total_buses=Bus.buses_count, rate=self.rate,
            num=self.people_transferred, total=Bus.people_transferred
        )
        return "Bus '{name} (rate: {rate} UAH)' (total: {total_buses}), " \
               "transferred {num} from {total} ppl".format(**data)
    
    # Adding method __repr__:
    __repr__ = info

b = Bus("Marshrutka #40")
b.transfer(100) # --> Bus.transfer(b, 100)
b.transfer(50)
print(b.info()) # --> Bus.info(b)
b3 = Bus("Tramway #1", 8)
Bus("Marshrutka #317")
b3.transfer(50)
#print(b2.__dict__)
print(b3.info())
# print(b) # if info() changed to __str__ or __repr__
print(f"Bus.people_transferred = {Bus.people_transferred}")
print(f"Bus.buses_count = {Bus.buses_count}")
print(f"Bus.buses = {Bus.buses}")
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Bus 'Marshrutka #40 (rate: 7 UAH)' (total: 1), transferred 150 from 150 ppl
    Bus 'Tramway #1 (rate: 8 UAH)' (total: 3), transferred 50 from 200 ppl
    Bus.people_transferred = 200
    Bus.buses_count = 3
    Bus.buses = [Bus 'Marshrutka #40 (rate: 7 UAH)' (total: 3), transferred 150 from 200 ppl, Bus 'Tramway #1 (rate: 8 UAH)' (total: 3), transferred 50 from 200 ppl, Bus 'Marshrutka #317 (rate: 7 UAH)' (total: 3), transferred 0 from 200 ppl]</code></span>


Creation of an instance of the class - like calling a function (in fact it is exactly like this - firstly we calling magic method `__new__()` then `__init__()`


```python
marshrutka_317 = Bus("# 317")
marshrutka_317.transfer(20)
print(marshrutka_317.info())
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Bus '# 317 (rate: 7 UAH)' (total: 4), transferred 20 from 220 ppl</code></span>



```python
b.transfer(23)
marshrutka_317.transfer()
marshrutka_317.transfer(55)  
print(marshrutka_317.info())
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Bus '# 317 (rate: 7 UAH)' (total: 4), transferred 76 from 299 ppl</code></span>


Class variables and instance variables were changed:


```python
print(Bus.people_transferred)
print(marshrutka_317.people_transferred)
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>299
    76</code></span>


## Inheritance


```python
class Robot:
    sounds = ["Beeep", "Bzzzt", "Oooooh"]
    
    def __init__(self, name, weigth=1000):
        self.weigth = weigth
        self.name = name
        
    def __str__(self):
        """Info about this robot"""
        return "Robot {obj.name} ({obj.weigth} kg)".format(obj=self)
 
    def say(self):
        """Say something"""
        import random 
        return f"{self.name} says: {random.choice(self.sounds)}"
```


```python
bip = Robot("Bip 1.0")
print(bip)
print(bip.say())
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Robot Bip 1.0 (1000 kg)
    Bip 1.0 says: Oooooh</code></span>


Let's say we need to create another type of robot. To reuse existing code we have to use Inheritance:


```python
class BendingRobot(Robot):
    sounds = ["Kill all humans", "Kiss my shiny metal face", "Oh, your God!",
              "Oh wait you’re serious. Let me laugh even harder."]
```


```python
bender = BendingRobot("Bender")
print(bender)
print(bender.say())          
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>Robot Bender (1000 kg)
    Bender says: Oh wait you’re serious. Let me laugh even harder.</code></span>


## Multiple Inheritance

Python supports a limited form of multiple inheritance as well. A class definition with multiple base classes looks like this:


```python
class A:
    a = "a from A"
    
class B(A):
    x = "x from B"
    
class C(A):
    a = "a from C"
    x = "x from C",
    
class D(B, C):  # change to D(C, B) and check...
    pass

d = D()
print(D.__mro__) # D.mro()
d.a, d.x
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)</code></span>





    ('a from C', 'x from B')



Let's enhance our `Robot` example by inheriting from two classes at once.


```python
class Mail:
    def send_message(self, msg):
        print(f"*** SENDING MESSAGE: <<<{msg}>>>  ***")
        
Mail().send_message("Test")
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>*** SENDING MESSAGE: <<<Test>>>  ***</code></span>



```python
class BendingMailingRobot(Robot, Mail):
    sounds = ["Kill all humans", "Kiss my shiny metal face", "Oh, your God!",
              "Oh wait you’re serious. Let me laugh even harder."]
    
bender2_0 = BendingMailingRobot("Bender 2.0")
bender2_0.send_message(bender2_0.say())
```

    *** SENDING MESSAGE: <<<Bender 2.0 says: Kill all humans>>>  ***


## Methods

Methods can be:
* instance methods
* class methods
* static methods

### Instance method

By default all methods (except of `__new__` are instance methods).

The method that should be called with the instance as it's first argument. This method is bound to instance so if calling as it's method passing instance is not required. Example:


```python
class Example:
    def cool_method(self):
        print(f"I am instance method, my instance is: {self}")
        
ex = Example()
ex.cool_method()
# Example.cool_method(ex)  # <-- same 

print(ex.cool_method)
```

    I am instance method, my instance is: <__main__.Example object at 0x7f343cf57ac8>
    <bound method Example.cool_method of <__main__.Example object at 0x7f343cf57ac8>>


### Class methods

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

    CLS: 5
    INSTANCE: 25
    CLS: 5


### Static method

This method doesn't require to pass instance/class at all.

To mark the method as static method it is required to use builtin decorator `@staticmethod`


```python
class Example:
    @staticmethod
    def cool_method():
        Example.attr = 123123
        print("I am a static method, I don't have access to anything :(")

    @staticmethod
    def other_stat_method(str_):
        return str_[::-1]
        
ex = Example()
ex.cool_method()
Example.cool_method()
ex.other_stat_method("Topot")
Example.attr
```

    I am a static method, I don't have access to anything :(
    I am a static method, I don't have access to anything :(





    123123



# Old and New classes

This chapter is only viable for Python 2 - as in Python 3 there are no such distinguishing as "old/new" classes.

Before Python 2.5 the format for creating a class was:

```python
class Old:
    pass
```
This was resulted in various problems with MRO and types. So some code redesigned, for this new format introduced:

```python
class New(object):
    pass
```

Differences:

1. `classobj` type as `builtin` types
2. Correct horizontal-then-vertical `MRO` (earlier it was vertical)
3. No `__new__()` method in old class
4. Additional functionality: 
    1. `__slots__` (Python 3.x)
    2. `__getattribute__`
    3. `__getattr__` and `__getattribute__` don't look for magic methods in instance