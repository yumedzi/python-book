# Basic Testing terminology

* Test scenario
* Test case
* Test

## Test Scenario

> Test scenario is the requirement for the application from the eyes of end-user

A test scenario is a small statement to verify one particular area of an application and these are mainly prepared after reviewing the functional requirements. 

## Test Case

A Test Case is a set of steps or conditions that a tester should follow to determine whether a particular feature or functionality of the software or application is working as per business requirement or not. 

Individual steps or intermidiate checks are tests or unit tests:

```sh
[ INPUT ] --->  [ PROGRAM ] ---> [ OUTPUT ] ---> [ CORRECT? ] ---> [ PASS or FAIL]
```

A formal test-case is usually described by a known input and by an expected output, which is compared to actual result during test execution. Comparing actual and expected is the result of the test case.

There are two main types of Test Cases:

* Positive Test Case
    * Verification based on the correct input 
* Negative Test Case
    * Verification based on the invalid or incorrect input

## Test

Test or Unit Test is a smallest part of Unit Test Case. 

Usually it checks some specific functionality of the module, class or method. Few unit test combined should form a Test Case which is testing particular feature of the program (that containes modules, classes and methods tested by various unit tests).

## The difference between Test Scenario and Test Case

> Test scenario is more general than Test case and usually contains many of them.

|Test Scenario/Case |Description|
|----|--------------|
| Test Scenario     | User can register in the system
| Test Case         | 1. User can register using Google SSO
| Test Case         | 2. User can register using Facebook SSO
| Test Case         | 3. User can register using email address


## The difference between Test Case and Test

> Test is the smallest part of the test case

|TestCase / Test    |Description|
|----|--------------|
| Test Case         | 3. User can register using email address
| Test              | 3.1. Registering with non-used email address and getting verification email
| Test              | 3.2. Validation of the activation from non-expired verification email
| Test              | 3.3. Validation of the activation from expired verification email
| Test              | 3.4. User can login using correct new account credentials
| Test              | 3.5. User can't login with correct new account credentials if verification period expired 
| Test              | 3.6. User can't login with incorrect new account credentials
| Test              | 3.7. Registering with used email address and getting error that login is already used