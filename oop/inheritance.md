# Inheritance

> It is possible for classes to inherit commonly used state attributes and methods described in other classes.

```python
class Robot(object):
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
        return "%s says: %s" % (self.name, random.choice(self.sounds))
```

```python
bip = Robot("Bip")
print(bip)
print(bip.say())  
```
Output:

    Robot Bip (1000 kg)
    Bip says: Bzzzt
    

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
Output:

    Robot Bender (1000 kg)
    Bender says: Oh, your God!
    

## Multiple Inheritance

Python supports a limited form of multiple inheritance as well. A class definition with multiple base classes looks like this:


```python
class A(object):
    a = 1
    
class B(A):
    x = 23
    
class C(A):
    a = 2
    
class D(B, C):
    pass

d = D()
d.a, d.x
```

Output:

    (2, 23)


