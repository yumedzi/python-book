# Testing theory

> Manual testing is the process through which software developers run tests manually, comparing program expectations and actual outcomes in order to find software defects.

> Automated testing is the process through which automated testing tools run tests that repeat predefined actions, comparing a developing program’s expected and actual outcomes.

What is the job of automated testing tools?
* verify code changes work out
* be helpful when tests fail 

Why do we need automated testing?
* to allow for later changes
* to raise confidence that code works
* to specify and document behaviour
* collaborative and faster development cycles

Some basic wise thoughts about tests:

* Should be in medium+ sized project!
* Each unit test should be doing only one test/assert (to find what is failing quicker).
* Should cover all possible scenarios/use cases.

Good tests should cover all possible scenarios/use cases:

<img width="500" src="images/tr_09_15.jpg">

... and sometimes even unbelievable:
<img width="600" src="images/tr_09_14.jpg">

## 7 testing principles

1. Testing shows the presence of defects, not their absence
2. Exhaustive testing is impossible
3. Early testing saves time and money
4. Defects cluster together
5. Beware of the pesticide paradox
6. Testing is context dependent
7. Absence-of-errors is a fallacy


## Types of testing:

* **Functional Testing**
    * The system is tested against the functional requirements/specifications.
* **Performance Testing** (also: Load Testing, Stress Testing): 
    * Evaluation of the performance of components.
* **Usability Testing**
    * How easily end user can operate with the application.
* **Security Testing**
    * Check for security vulnerabilities and the level of data protection in the system.
* **Portability Testing**
    * Check how reliably does the software work in a specific environment.

### Functional Testing

Functional Testing verifies that each function of the software application operates in conformance with the requirement specification. Functional testing is a quality assurance (QA) process and mainly involves Black Box Testing. It is concerned about the results of processing and not about the source code of the application.
    
Most well-known levels of FT:
    
* **Unit testing**
    * units react well to input
* **integration**: 
    * unit/components co-operate nicely
* **system**: 
    * everything altogether is working OK
* **acceptance**:
    * full system on production

All levels of Functional Testing:

* Unit Testing: Individually and independently testing of smallest testable parts of an application
* Integration Testing: When individual software modules are combined together and tested as a group.
* System Testing: Testing conducted on a complete, integrated system to evaluate the system’s compliance with its specified requirements.
* Sanity Testing: Very brief run-through of the functionalities to assure that part of the system or methodology works roughly as expected.
* Regression Testing: Retesting of a software system to confirm that changes made to few parts of the codes has not any side affects on existing system functionalities.
* Acceptance Testing:  Formal testing with respect to user needs, requirements, and business processes conducted to determine whether a system satisfies the acceptance criteria.
* Alpha & Beta Testing: Alpha Testing is conducted by a team of highly skilled testers at development site whereas Beta Testing is always conducted in Real Time environment by customers or end users at their own site.


### Unit Testing

> A **unit** is the smallest testable part of an application like functions, classes. 

> Unit Testing is a Software Testing method by which individual units of source code are tested.

The idea of Unit Testing is to split the program into smallest bits and test them individually. This usually means that each specific module, class or function is tested by giving it the number of inputs and comparing the actual results with expected values.

Pluses:
* Easy to spot a bug
* Easy to debug

### Unit, Integration and System Testing

Unit, Integration and System Testing cover main part of application life cycle:

* Each component works OK ⟶ Unit Testing
* Components are working together OK ⟶ Integration Testing
* System itself working OK ⟶ System Testing