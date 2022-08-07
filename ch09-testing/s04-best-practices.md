## Unit test design best practices


Characteristics of a good unit test:

* Fast. It is not uncommon for mature projects to have thousands of unit tests. Unit tests should take very little time to run. Milliseconds.
* Isolated. Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
* Repeatable. Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.
* Self-Checking. The test should be able to automatically detect if it passed or failed without any human interaction.
* Timely. A unit test should not take a disproportionately long time to write compared to the code being tested. If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.



## Naming

The name of the unit test should ideally consist of some of these parts:

* The name of the method being tested.
* The unique test ID
* The scenario under which it's being tested.
* The expected behavior when the scenario is invoked.

In the end this is always up to specific project's convention but having definitive naming helps.

Consider the diff of:

🪄 _<mark style="color:green;">Code:</mark>_

```python
def test_15(self):
   self.assertEqual(func(500), 1000)
```

and:

🪄 _<mark style="color:green;">Code:</mark>_

```python
def test_15_func_with_num__returns_double(self):
   self.assertEqual(func(500), 1000)
```


## Unit test structure

`AAA` (Arrange, Act, Assert) is a common pattern when unit testing:

* Arrange your objects, creating and setting them up as necessary.
* Act on an object.
* Assert that something is as expected.


🪄 _<mark style="color:green;">Code:</mark>_

```python
def test_15_method_with_num__returns_double(self):
    # Arrange
    some_obj = TestClass()
    
    # Act
    actual = some_obj.method(test_value=500)
    
    # Assert
    self.assertEqual(actual, 1000)
```   

### Coverage

The unit test should cover main aspects of the program:

* Positive tests:
    * "Normal" flow of the program - normally expected types of input parameters
* Negative tests:
    * Different, not expected, types of input parameters of the test function, empty sequences, `0`, `None` etc.
    * Checking that the test function raises expected error/exception


> It is possible to measure the level of coverage of unit tests by using `coverage` 3rd party module (check `Pytest` section below for more details).

### Avoid logic in tests

When writing the unit tests avoid logic and data processing as much as possible.

Try to avoid:
* string concatenation
* logical conditions
* loop
    * except the case you are testing each item from fixture
    
Of course, this recommendation is idealistic but having extra place of possible error is bad in the long run.

### Avoid multiple asserts

When writing the unit tests, try to only include one assert per test because otherwise it will difficult to pinpoint the issue:

* Create a separate test for each assert.
* Use parameterized tests (`pytest`).