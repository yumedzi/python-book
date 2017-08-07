# OOP basics

> OOP (Object oriented Programming) - programming paradigm where all operations are based on manipulations on abstract objects which has internal state and support methods that query or modify this internal state in some way.

Python’s class mechanism adds classes with a minimum of new syntax and semantics. 

Python classes provide all the standard features of Object Oriented Programming: the class inheritance mechanism allows multiple base classes, a derived class can override any methods of its base class or classes, and a method can call the method of a base class with the same name. Objects can contain arbitrary amounts and kinds of data. As is true for modules, classes partake of the dynamic nature of Python: they are created at runtime, and can be modified further after creation.

Main OOP terms:
* Classes, objects/instances
* Methods
* Instantiation
* Inheritance
* Method overloading

## OOP mini glossary

* **Class**
    * "An idea" of object, some pattern
    * A user-defined prototype for an object that defines a set of attributes that characterize any object of the class.
    * Logical group of data (attributes) and functions (referred to as "methods" when defined within a class)
   
* **Instance**
    * An individual object of a certain class.

* **Method**:
    * A special kind of function that is defined in a class definition.

* **Inheritance**: 
    * Passing attributes and methods of a parent class to instance or child class

* **Method overloading**: 
    * The assignment of more than one behavior to a particular method

## 4 principles of OOP

* Encapsulation
* Data Abstraction
* Inheritance
* Polymorphism

### Encapsulation 

* A language mechanism for restricting direct access to some of the object's components.
* A language construct that facilitates the bundling of data with the methods (or other functions) operating on that data.

### Data Abstraction

Abstraction is a technique for managing complexity of computer systems. It works by establishing a level of complexity on which a person interacts with the system, suppressing the more complex details below the current level.

### Inheritance

Inheritance is a way to reuse code of existing objects, or to establish a subtype from an existing object, or both, depending upon programming language support. In classical inheritance where objects are defined by classes, classes can inherit attributes and behavior from pre-existing classes called base classes, superclasses, parent classes or ancestor classes. 

### Polymorphism

Polymorphism means one name, many forms. Polymorphism manifests itself by having multiple methods all with the same name, but slightly different functionality.

There are 2 basic types of polymorphism.
Overridding, also called run-time polymorphism. For method overloading, the compiler determines which method will be executed, and this decision is made when the code gets compiled.
Overloading, which is referred to as compile-time polymorphism. Method will be used for method overriding is determined at runtime based on the dynamic type of an object.
