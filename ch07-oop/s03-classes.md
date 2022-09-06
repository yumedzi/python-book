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

### Simple OOP examples

Here is the simplest class for Cat and two objects of this class:


🪄 <mark style="color:red;">Code</mark>:

```python
class Cat:
    pass 

agata = Cat()
blanka = Cat()

print(agata, id(agata))
print(blanka, id(blanka))
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<__main__.Cat object at 0x7f6dddf02380> 140109851665280
<__main__.Cat object at 0x7f6dddf03cd0> 140109851671760
```
{% endcode %}
Cat class and object is "empty" - doesn't define any attributes and methods. They even don't have their proper name.

Let's add names:


🪄 <mark style="color:red;">Code</mark>:

```python
agata.name = "Agata"

print(agata.name)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Agata
```
{% endcode %}
We can assign attributes during initialization of the object - it would simplify things a lot.

The method starts with `__` ("dunder") is called a magic method. `__init__` is one example, `__str__` - method that defines a string representation of the object - is another.

`self` in examples below is the reference to the object itself so we could use it in the function code - for example during `str(agata)` Python will call `agata.__str__()` which will need to return a string including `agata.name`, and it does this using the reference `self`.


🪄 <mark style="color:red;">Code</mark>:

```python
class Cat:
    def __init__(self, name="Stray"):
        self.name = name
        
    def __str__(self):
        return f'<Cat "{self.name}">'
        
agata = Cat("Agata")
street_cat = Cat()

print(agata)
print(street_cat)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<Cat "Agata">
<Cat "Stray">
```
{% endcode %}
Magic methods are not the only ones we can define - in fact we can add any method that would describe some action involving an object.

Here we also will set a class attribute accessible from all children.


🪄 <mark style="color:red;">Code</mark>:

```python
class Cat:
    default_sound = "Meow"
    
    def __init__(self, name="Stray"):
        self.name = name
        #self.default_sound = "Rrrr"  # We can override "global" class attribute with "local" instance attribute
        
    def __str__(self):
        return f'<Cat "{self.name}">'
    
    def sound(self, times=3):
        return " ".join([self.default_sound] * times)
    
blanka = Cat("Blanka")
print(blanka.sound())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Meow Meow Meow
```
{% endcode %}
Examples with more methods/attributes:


```python
class Bus:
    """ Sample Bus class """
    # Class attributes
    buses_count = 0
    people_transferred = 0
    money_collected = 0
    buses = []
 
    # Instance Initializer
    def __init__(self, name="Some Bus", rate=7):
        # instance attribute
        self.name = name
        self.people_transferred = 0
        self.rate = rate
        self.money_collected = 0
        Bus.buses_count += 1  # self.__class__.buses_count += 1
        Bus.buses.append(self)
 
    # Instance method
    def transfer(self, num=1):
        self.people_transferred += num
        self.__class__.people_transferred += num
        self.money_collected += self.rate * num
        self.__class__.money_collected += self.rate * num
        
    def __str__(self):
        return f"<Bus '{self.name}'>"
 
    def info(self): # change to __str__
        data = dict(
            name=self.name, total_buses=Bus.buses_count, rate=self.rate,
            num=self.people_transferred, total=Bus.people_transferred
        )
        return "Bus '{name}' (rate: {rate}€) (total: {total_buses}), " \
               "transferred {num} from {total} ppl".format(**data)
    
    def __repr__(self):
        return f"Bus('{self.name}', {self.rate})"
```


```python
b = Bus("Bus #40")
b.transfer(100) # --> Bus.transfer(b, 100)
```


```python
b
```




📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus('Bus #40', 7)
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
print(b)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
<Bus 'Bus #40'>
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
b.transfer(50)
print(b.info()) # --> Bus.info(b)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus 'Bus #40' (rate: 7€) (total: 1), transferred 150 from 150 ppl
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
b2 = Bus("Tram #1", 8)
b2.transfer(50)
print(b2.info())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus 'Tram #1' (rate: 8€) (total: 2), transferred 50 from 200 ppl
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
print(f"Bus.people_transferred = {Bus.people_transferred}")
print(f"Bus.money_collected = {Bus.money_collected}")
print(f"Bus.buses_count = {Bus.buses_count}")
print(f"Bus.buses = {Bus.buses}")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus.people_transferred = 200
Bus.money_collected = 1450
Bus.buses_count = 2
Bus.buses = [Bus('Bus #40', 7), Bus('Tram #1', 8)]
```
{% endcode %}
Creation of an instance of the class - like calling a function (in fact it is exactly like this - firstly we calling magic method `__new__()` then `__init__()`


🪄 <mark style="color:red;">Code</mark>:

```python
bus_317 = Bus("# 317")
bus_317.transfer(20)
print(bus_317.info())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus '# 317' (rate: 7€) (total: 3), transferred 20 from 220 ppl
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
b.transfer(23)
bus_317.transfer()
bus_317.transfer(55)  
print(bus_317.info())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Bus '# 317' (rate: 7€) (total: 3), transferred 76 from 299 ppl
```
{% endcode %}
Class variables and instance variables were changed:


🪄 <mark style="color:red;">Code</mark>:

```python
print(Bus.people_transferred)
print(bus_317.people_transferred)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
299
76
```
{% endcode %}
## Inheritance

Inheritance from some class (called "base" or `super` class) allows to create a new class "borrowing" all attributes and methods definitions as they were in the super class. It allows to:

1. Reuse the code (DRY principle).
2. Create abstractions.

For example here is the class for the Robot:


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

It is completely usable:


🪄 <mark style="color:red;">Code</mark>:

```python
bip = Robot("Bip 1.0")
print(bip)
print(bip.say())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Robot Bip 1.0 (1000 kg)
Bip 1.0 says: Bzzzt
```
{% endcode %}
We can re-use this class to create a robot from Futurama using the inheritance. For this we need to specify base/super class in parenthesis during new class definition.


```python
class BendingRobot(Robot):
    sounds = ["Kill all humans", "Kiss my shiny metal face", "Oh, your God!",
              "Oh wait you’re serious. Let me laugh even harder."]
```


🪄 <mark style="color:red;">Code</mark>:

```python
bender = BendingRobot("Bender")
print(bender)
print(bender.say())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
Robot Bender (1000 kg)
Bender says: Kiss my shiny metal face
```
{% endcode %}
As we can we still can use `say` method defined in the base class.

## Multiple Inheritance

Python supports a limited form of multiple inheritance as well. A class definition with multiple base classes looks like this:


🪄 <mark style="color:red;">Code</mark>:

```python
class A:
    a = "a from A"[]
    
class B(A):
    x = "x from B"
    
class C(A):[]
    a = "a from C"
    x = "x from C",
    
class D(B, C):  # change to D(C, B) and check...
    pass

d = D()
print(D.__mro__) # D.mro()
print(d.a, d.x)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
a from C x from B
```
{% endcode %}
Let's enhance our `Robot` example by inheriting from two classes at once.


🪄 <mark style="color:red;">Code</mark>:

```python
class Mail:
    def send_message(self, msg):
        print(f"*** SENDING MESSAGE: <<<{msg}>>>  ***")
        
Mail().send_message("Test")
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
*** SENDING MESSAGE: <<<Test>>>  ***
```
{% endcode %}
🪄 <mark style="color:red;">Code</mark>:

```python
class BendingMailingRobot(Robot, Mail):
    sounds = ["Kill all humans", "Kiss my shiny metal face", "Oh, your God!",
              "Oh wait you’re serious. Let me laugh even harder."]
    
bender2_0 = BendingMailingRobot("Bender 2.0")
bender2_0.send_message(bender2_0.say())
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
*** SENDING MESSAGE: <<<Bender 2.0 says: Oh wait you’re serious. Let me laugh even harder.>>>  ***
```
{% endcode %}
More advanced example:


🪄 <mark style="color:red;">Code</mark>:

```python
class BendingMailingRobot(Robot, Mail):
    sounds = ["Kill all humans", "Kiss my shiny metal face", "Oh, your God!",
              "Oh wait you’re serious. Let me laugh even harder."]
    
    def mail(self):
        return self.send_message(self.say())
    
bender3_0 = BendingMailingRobot("Bender 3.0")
bender3_0.mail()
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
*** SENDING MESSAGE: <<<Bender 3.0 says: Oh, your God!>>>  ***
```
{% endcode %}
## Methods

Methods can be:
* instance methods
* class methods
* static methods

### Instance method

By default all methods (except of `__new__` are instance methods).

The method that should be called with the instance as it's first argument. This method is bound to instance so if calling as it's method passing instance is not required. Example:


🪄 <mark style="color:red;">Code</mark>:

```python
class Example:
    def cool_method(self):
        print(f"I am instance method, my instance is: {self}")
        
ex = Example()
ex.cool_method()
# Example.cool_method(ex)  # <-- same 

print(ex.cool_method)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
I am instance method, my instance is: <__main__.Example object at 0x7f6ddd803400>
<bound method Example.cool_method of <__main__.Example object at 0x7f6ddd803400>>
```
{% endcode %}
### Class methods

The method with class as the first argument. Useful to run some code without need of creating the instace. 

To mark the method as class method it is required to use builtin decorator `@classmethod`


🪄 <mark style="color:red;">Code</mark>:

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

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
CLS: 5
INSTANCE: 25
CLS: 5
```
{% endcode %}
### Static method

This method doesn't require to pass instance/class at all.

To mark the method as static method it is required to use builtin decorator `@staticmethod`


🪄 <mark style="color:red;">Code</mark>:

```python
class Example:
    @staticmethod
    def cool_method():
        Example.attr = 123123
        return "I am a static method, I don't have access to anything :("

    @staticmethod
    def other_stat_method(str_):
        return str_[::-1]
        
ex = Example()
print(ex.cool_method())
print(Example.cool_method())
print(ex.other_stat_method("Radar"))
print(Example.attr)
```

📟 <mark style="color:green;">Output</mark>:

{% code overflow="wrap" %}
```
I am a static method, I don't have access to anything :(
I am a static method, I don't have access to anything :(
radaR
123123
```
{% endcode %}
# Old and New classes

> This chapter is only viable for Python 2 - as in Python 3 there are no such distinguishing as "old/new" classes.

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