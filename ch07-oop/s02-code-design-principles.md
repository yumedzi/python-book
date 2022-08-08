# Code design principles

Here we will cover the following important principles (lot of abbreviations):
* DRY
* KISS
* SOLID
    * SRP
    * OCP
    * LSP
    * ISP
    * DIP

### Don't Repeat Yourself (DRY)

> Not the part of SOLID, but still - very important principle

* Avoid duplicate code by abstracting out things that are common and placing those things in a single location.
* DRY is about having each piece of information and behavior in your system in a single, sensible place.

Violating DRY:
* "We enjoy typing"
* "Wasting everyone's time"

## Keep It Simple, Stupid (KISS)

Keep the code simple and clear, making it easy to understand. All code is written for humans not computes after all.

* Keep your methods small. 
* Each method should never be more than 20 lines.
    * If you see the function/method is growing too big - think of making another function that will cover part of this (it would be great if this part would be re-used).
* Don't use OOP for everything.
    * Python is multi-paradigm language so use what's best for the task.

## [SOLID](https://deviq.com/solid/) principles of Object Oriented Design

* _SRP_ – **S**ingle Responsibility Principle
  * Class has one job to do. Each change in requirements can be done by changing just one class.
* _OCP_ – **O**pen/Closed Principle
  * Classes should be open for extensions (inheritance), but closed for modification.
* _LSP_ – **L**iskov Substitution Principle
  * Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.
* _ISP_ – **I**nterface Segregation Principle
 * Clients should not be forced to depend upon interfaces that they do not use.
* _DIP_ – **D**ependency Inversion Principle
 * Depend upon abstractions, \[not\] concretions.

### Single Responsibility Principle

Every object in your system should have a single responsibility, and all the object's services should be focused on carrying out that single responsibility.

If the class will cover a lot of different functionality changing one of them could potentially break other meaning such a class is hard to manage, develop and test. When the class is all about one domain application functionality - the changes are easier to make and test.

### Open-Closed Principle

Classes should be open for extension, and closed for modification.

Business needs change very often and in a variety of ways. Changing the base class to accomodate to such changes meaning overloading the code with all of cornercases, checks, conditions. This will lead to a chaotic code which will extremely hard to maintain and test. In accordance with `OCP` principle the classes should be extended (via inheritance) to cover additional usecases and scenarios.

### Liskov Substitution Principle

Subtypes must be substitutable for their base types. This helps with understandability, testing, scalability and management.

When this principle is violated, it tends to result in a lot of extra conditional logic scattered throughout the application, checking to see the specific type of an object.

### Interface Segregation Principle 

* Clients should not be forced to depend on methods that they do not use.
* Interfaces should belong to clients, not to libraries or hierarchies. 

Application developers should favor thin, focused interfaces to "fat" interfaces that offer more functionality than a particular class or method needs.

For Python world: 
* Do not put all possible methods in a base class if not all inherited classes will use them all.
* Better to segregate - create a few base classes with small functionality that will be used.

### Dependency inversion principle

> This is my favorite :)

* High-level modules should not import anything from low-level modules. Both should depend on abstractions.
* Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

For Python world this means:
* Business logic should not depend on low-level code (like handling database, filesystem, etc.). If those low-level components need to be changed this won't break most important logic.
* Business logic can depend on some abstraction. 

For example our code (file backuper) depends on real file system to read and manage files. We can use DIP principle to substitute ths dependency with some abstract class that needs to have used methods like `read`, `copy` etc. Then we can inherit that class and create a class to handle local filesystem or in the future - remote or cloud storages - without changing anything in the main business logic.

This helps to loose coupling making the code more maintainable and testable.