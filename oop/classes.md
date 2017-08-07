# Classes and instances

Classes created with operator `class`:
 
```python 
class A(object):
    attr = 10
```
 
When a class definition is entered, a new namespace is created, and used as the local scope — thus, all assignments
to local variables go into this new namespace. In particular, function definitions bind the name of the new function here

Class objects support two kinds of operations: attribute references and instantiation.


```python
class Bus(object):
    """ Sample Bus class """
    # Class attributes
    buses_count = 0
    people_transferred = 0
 
    # Instance Initializer
    def __init__(self, name="Some Bus"):
        # instance attribute
        self.name = name
        self.people_transferred = 0
        Bus.buses_count += 1
 
    # Instance method
    def transfer(self, num=1):
        self.people_transferred += num
        Bus.people_transferred += num
 
    def info(self): # change to __str__
        data = dict(
            name=self.name, total_buses=Bus.buses_count,
            num=self.people_transferred, total=Bus.people_transferred)
        return "Bus '{name}' (total: {total_buses}), " \
               "transferred {num} from {total} ppl".format(**data)

b = Bus("Marshrutka #40")
b.transfer(100) # --> Bus.transfer(b, 100)
b.info() # --> Bus.info(b)
```

Output:


    "Bus 'Marshrutka #40' (total: 1), transferred 100 from 100 ppl"



Creation of an instance of the class - like calling a function (in fact it is exactly like this - firstly we calling magic method `__new__()` then `__init__()`


```python
marshrutka_317 = Bus("# 317")
marshrutka_317.transfer(20)
print(marshrutka_317.info())
```
Output:

    Bus '# 317' (total: 2), transferred 20 from 120 ppl
    


```python
b.transfer(23)
marshrutka_317.transfer()
marshrutka_317.transfer(55)  
print(marshrutka_317.info())
```
Output:

    Bus '# 317' (total: 2), transferred 77 from 200 ppl
    

Class variables and instance variables were changed:


```python
print(Bus.people_transferred)
print(marshutka_317.people_transferred)
```
Output:

    79
    56
    
