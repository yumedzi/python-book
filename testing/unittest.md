# Unittest

> Classic Python testing 

* Production-ready powerful testing framework
* Batteries-included test module in the Python standard library.

## Main terminology:

* test
    * Smallest unit of testing. Function for testing specific (ideally) smallest piece of functionality.
* test case
    * A test case is the collection of tests combined by some common meaning/feature. It checks for a specific response to a particular set of inputs. unittest provides a base class, TestCase.
* test fixture
    * A test fixture represents the preparation needed to perform one or more tests, and any associate cleanup actions.
* test suite
    * A test suite is a collection of test cases, test suites, or both.
* test runner
    * A test runner is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.

## Usage

1. Define your own class derived from unittest.TestCase.
2. Filling it with functions that start with `test_` 
3. Run the tests by placing unittest.main() in a file, usually at the bottom:

```python
if __name__ == '__main__':
    unittest.main()
```

Example of simple testing:

```python
import unittest

class TestStringMethods(unittest.TestCase):
    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')
        
    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())
        
    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```

Output:

    ...
    ----------------------------------------------------------------------
    Ran 3 tests in 0.005s
    
    OK
    


Tests have different outcomes:

|Status| Decription |
|--|---------------------|
|. |ok
|F |Fail
|E |Error
|x |expected failure
|s |skipped 'msg'
|u |unexpected success

## Testing of sample code

Let's cover the following OOP sample code with tests (let's assume it is `"main.py"`):

```python
from random import choice

class Monkey:
    name = None
    age = None
    actions = ['saying "Boo boo boo"', 'dancing rock&roll', 
               'jumping like a crazy frog' ]
    
    def __init__(self, name="Boo", age=2):
        self.name = name
        self.age = age
        
    def trick(self):
        return "%s is %s" % (self.name, choice(Monkey.actions))
```

We can create some `"test.py"` with the following code:

```python
import unittest

from main import Monkey


class MonkeyTestCase(unittest.TestCase):
    def test_naming(self):
        monkey = Monkey('Foo', 3)
        self.assertEqual(monkey.name, 'Foo')
    
    def test_aging(self):
        monkey = Monkey('Foo', 3)
        self.assertEqual(monkey.age, 3)
    
    def test_action(self):
        monkey = Monkey('Foo', 3)
        self.assertEqual(monkey.trick(), 'Foo is saying "Boo boo boo"')
    
if __name__ == '__main__':
    unittest.main()

```
Output:

    ...
    ----------------------------------------------------------------------
    Ran 3 tests in 0.006s
    
    OK


How can we optimize the tests above?

First of all - by removing redundancy.


```python
class MonkeyTestCase(unittest.TestCase):
    def setUp(self):
        self.monkey = Monkey('Foo', 3)
    def tearDown(self):
        del self.monkey
        
    def test_naming(self):
        self.assertEqual(self.monkey.name, 'Foo')
    def test_aging(self):
        self.assertEqual(self.monkey.age, 3)
    def test_action(self):
        self.assertEqual(self.monkey.trick(), 'Foo is saying "Boo boo boo"') 
        
suite = unittest.TestLoader().loadTestsFromModule(MonkeyTestCase())
unittest.TextTestRunner().run(suite)   
```
Output:

    ...
    ----------------------------------------------------------------------
    Ran 3 tests in 0.006s
    
    OK


33% chance that we will get this:

```shell
$ python test.py –v
test_action (__main__.MonkeyTestCase) ... ok
test_aging (__main__.MonkeyTestCase) ... ok
test_naming (__main__.MonkeyTestCase) ... ok
--------------------------------------------------
Ran 3 tests in 0.000s
OK
```


In most cases unit tests should not contain more than one assertion.

* The idea is that each unit test should test one thing and one thing only, to further narrow down what the problem is, when the test fails.


* Optimum approach:
    * test function can have any number of trivial assertions, and at most one non-trivial assertion

Each test is a method, each test naturally runs in its own variable scope. We gain a big advantage from keeping the tests isolated

`assert<SomeCheckMethod>` methods from `TestCase`. These give us more flexible ways of checking whether values match, and provide more useful error reports, than Python's basic assert statement.

| Assert method  |         Meaning    |
|----------------|--------------------|
| `assertEqual(a, b)` | `a == b`
| `assertNotEqual(a, b)` | `a != b`
| `assertAlmostEqual(a, b)` | `a == b` (almost `:)`)
| `assertNotAlmostEqual(a, b)` | `a != b` (emm.., almost!)
| `assertTrue(x)` | `bool(x) is True`
| `assertFalse(x)` | `bool(x) is False`
| `assertIs(a, b)` | `a is b`
| `assertIsNot(a, b)` | `a is not b`
| `assertIsNone(x)` | `x is None`
| `assertIsNotNone(x)` | `x is not None`
| `assertIn(a, b)` | `a in b`
| `assertNotIn(a, b)` | `a not in b`
| `assertIsInstance(a, b)` | `isinstance(a, b)`
| `assertNotIsInstance(a, b)` | `not isinstance(a, b)`

## Examples

```python
from unittest import TestCase

class LordOfTheFails(TestCase):
    def test_1_plus_1__2(self):
        self.assertTrue(1 == 1 + 1)
    
    def test_1_plus_1__1(self):
        self.assertNotEqual(1, 1 + 1) 
        
```
Output:
```shell
FF
======================================================================
FAIL: test_1_plus_1__1 (__main__.LordOfTheFails)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-82-0cb63d3671d1>", line 8, in test_1_plus_1__1
    self.assertEqual(1, 1 + 1)
AssertionError: 1 != 2

======================================================================
FAIL: test_1_plus_1__2 (__main__.LordOfTheFails)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-82-0cb63d3671d1>", line 5, in test_1_plus_1__2
    self.assertTrue(1 == 1 + 1)
AssertionError: False is not true

----------------------------------------------------------------------
Ran 2 tests in 0.007s

FAILED (failures=2)
```

Processing floating point numbers can be a pain:

```python
class FloatingProblems(TestCase):
    def test_root_incorrect(self):
        self.assertEqual((7.0 ** 0.5) ** 2.0, 7.0)
        
    def test_root_correct(self):
        self.assertAlmostEqual((7.0 ** 0.5) ** 2.0, 7.0)
        
``` 
Output:
```shell
.F
======================================================================
FAIL: test_root_incorrect (__main__.FloatingProblems)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-84-19f2cfae6434>", line 3, in test_root_incorrect
    self.assertEqual((7.0 ** 0.5) ** 2.0, 7.0)
AssertionError: 7.000000000000001 != 7.0

----------------------------------------------------------------------
Ran 2 tests in 0.007s

FAILED (failures=1)
```

WHAT???

`AssertionError: 7.000000000000001 != 7.0`

* Pretty frustrating, isn't it?

* Try:
```python
2.2 * 3.0 == 6.6
3.3 * 2.0 == 6.6
```

Checking exceptions:
    
```python
class ExceptionShowCase(TestCase):
    def test_int_from_string(self):
        self.assertRaises(ValueError, int,
                          '31415HELPIAMTRAPPED32', base = 16)
    
    def test_int_from_string_2(self):
        fail = lambda: int('31415HELPIAMTRAPPED32', base = 16)
        self.assertRaises(ValueError, fail)
        
    def test_nice_int_from_str(self):
        with self.assertRaises(SomeException):
            int('31415HELPIAMTRAPPED32', base = 16)
        
```

> **Error** not a Fail will be reported in case of exception type mismatch!


More batteries!

What should we use when EVERYTHING in assert methods are not good for us (it's near to impossible btw)?

* Just fail the test! 
* `self.fail()`

```python
class TimeMachineTest(TestCase):
    def test_time_machine(self):
        from datetime import datetime as dt
        if dt.now().year != 1986:
            self.fail("Hmm, Time Machine has been broken!")
```

Let's fix the third test - with our super knowledge!

```python
def test_action(self):
    self.assertEqual(self.monkey.trick(), 'Foo is saying "Boo boo boo"')
```

How should it look like?

```python
def test_action(self):
    self.assertIn(
        self.monkey.trick(),
        ['{0.name} is {1}'.format(self.monkey, x) for x in Monkey.actions]
    )
```

### Test Fixtures

* Fixtures are resources needed by a test.
* To configure the fixtures, override `setUp()` ->  will be run BEFORE EACH TEST
* To clean up, override `tearDown()` ->  will be run AFTER EACH TEST

```python
def setUp(self):
    self.monkey = Monkey('Foo', 3)
    
def tearDown(self):
    del self.monkey
```

* Per test case:
    * Override `setUpClass()` -> will be run ONCE for testcase
    * To clean up, override `tearDownClass()` -> will be run ONCE for testcase

```python
@classmethod
def setUpClass(cls):
    cls.monkey = Monkey('Foo', 3)

@classmethod
def tearDownClass(cls):
    del cls.monkey
```


### Test suites

* Used to organize many tests
* Not used often, better use lib 'nose'
* Instead of unittest.main(), there are other ways to run the tests with a finer level of control, less terse output, and no requirement to be run from the command line. 

For example: 

```python
from unittest import TestLoader, TextTestRunner
suite = TestLoader().loadTestsFromTestCase(LordOfTheFails)
unittest.TextTestRunner(verbosity=2).run(suite)
```