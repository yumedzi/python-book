# Unittest

> Classic Python testing 

* Powerful framework for testing
* Batteries-included test module in the Python standard library.

Usage

1. Define your own class inherited from `unittest.TestCase`.
2. Filling it with methods with names starting with `test_` 
3. Run the tests by placing `unittest.main()` in a file, usually at the bottom:

```python
if __name__ == '__main__':
    unittest.main()
```

## Main terminology:

* test
    * Smallest unit of testing. Function for testing specific (ideally) smallest piece of functionality.
* test case
    * A test case is the collection of tests combined by some common meaning/feature. It checks for a specific response to a particular set of inputs. `unittest` provides a base class, `TestCase`.
* test fixture
    * A test fixture represents the preparation needed to perform one or more tests, and any associate cleanup actions.
* mocking
    * An operation of emulating some object's attribute or the result returned by arbitrary method to be able to test the functionality of tested unit in different conditions.
* test suite
    * A test suite is a collection of test cases, test fixtures, or both.
* test runner
    * A test runner is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.


```python
import unittest

class TestStringMethods(unittest.TestCase):
    def test_001_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')
        
    def test_011_isupper(self):
        self.assertTrue('FOO'.isupper(), "Subtest 011-01: check upper")
        self.assertTrue('foo'.islower(), "Subtest 011-02: check lower")
        
    def test_012_isupper(self):
        self.assertFalse('Foo'.isupper())
        
    def test_021_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        
    def test_022_split(self):
        s = 'hello world'
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
import unittest

class TestStringMethods(unittest.TestCase):
    @unittest.expectedFailure
    def test_01_upper(self):
        self.assertEqual('fooooool000'.lower(), 'FOOOOOO1000'.lower(), "Non-critical Python string handling error")

    def test_02_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())
        
    def test_03_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    suite = unittest.TestLoader().loadTestsFromModule(TestStringMethods())
    unittest.TextTestRunner(verbosity=1).run(suite)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
x..
----------------------------------------------------------------------
Ran 3 tests in 0.011s
```
{% endcode %}

    
    OK (expected failures=1)


Result:

```
$ python super_script.py -v
test (__main__.SomeTest) ... ok
----------------------------------------------------------
Ran 1 test in 0.000s
OK
```

Tests have different outcomes:

|Status| Decription |
|--|---------------------|
|. |ok
|F |Fail
|E |Error
|s |skipped 'msg' - @unittest.skip("demo") 
|x |expected failure  - @unittest.expectedFailure
|u |unexpected success



```python
from random import choice

class Monkey:
    actions = ['saying "Boo boo boo"', 'dancing rock&roll', 
               'jumping like a crazy frog']
    
    def __init__(self, name="Dummy Monkey", age=2):
        self.name = name
        self.age = age
        
    def action(self):
        return " is ".join((self.name, choice(self.actions)))
```


🪄 _<mark style="color:green;">Code:</mark>_

```python
import unittest

class MonkeyTestCase(unittest.TestCase):
    def test_naming(self):
        monkey = Monkey('Foo', 3)
        self.assertEqual(monkey.name, 'Foo')
    
    def test_aging(self):
        monkey = Monkey('Foo', 3) 
        self.assertEqual(monkey.age, 3)
    
    def test_action(self):
        monkey = Monkey('Foo', 3)
        self.assertEqual(monkey.action(), 'Foo is saying "Boo boo boo"')
     
suite = unittest.TestLoader().loadTestsFromModule(MonkeyTestCase())
unittest.TextTestRunner().run(suite)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
F..
======================================================================
FAIL: test_action (__main__.MonkeyTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-15-4b4fd808bbe2>", line 14, in test_action
    self.assertEqual(monkey.action(), 'Foo is saying "Boo boo boo"')
AssertionError: 'Foo is jumping like a crazy frog' != 'Foo is saying "Boo boo boo"'
- Foo is jumping like a crazy frog
+ Foo is saying "Boo boo boo"
```
{% endcode %}

    
    
    ----------------------------------------------------------------------
    Ran 3 tests in 0.011s
    
    FAILED (failures=1)





    <unittest.runner.TextTestResult run=3 errors=0 failures=1>



How can we optimize the tests above?

First of all - by removing redundancy.


🪄 _<mark style="color:green;">Code:</mark>_

```python
class MonkeyTestCase(unittest.TestCase):
    def setUp(self):
        self.monkey = Monkey('Foo', 3)

    def tearDown(self):
        del self.monkey
        
    def test_01_naming(self):
        self.assertEqual(self.monkey.name, 'Foo')
        
    def test_02_aging(self):
        self.assertEqual(self.monkey.age, 3)
        
    def test_03_action(self):
        self.assertEqual(self.monkey.action(), 'Foo is saying "Boo boo boo"') 
        
suite = unittest.TestLoader().loadTestsFromModule(MonkeyTestCase())
unittest.TextTestRunner(verbosity=1).run(suite)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
...
----------------------------------------------------------------------
Ran 3 tests in 0.013s
```
{% endcode %}

    
    OK





    <unittest.runner.TextTestResult run=3 errors=0 failures=0>



**33%** chance that we got this:

```shell
$ python test_example2.py –v
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
| `assertAlmostEqual(a, b)` | almost equal `:)`)
| `assertNotAlmostEqual(a, b)` | not almost equal
| `assertTrue(x)` | `bool(x) is True`
| `assertFalse(x)` | `bool(x) is False`
| `assertIs(a, b)` | `a is b`

| Assert method  |         Meaning    |
|----------------|--------------------|
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
    def test_1_plus_1__1(self):
        self.assertEqual(1, 1 + 1) 
    
    def test_1_plus_1__2(self):
        self.assertTrue(1 == 1 + 1)        
```

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

Processing floating point numbers can be a pain

```python
class FloatingProblems(TestCase):
    def test_root_incorrect(self):
        self.assertEqual((7.0 ** 0.5) ** 2.0, 7.0)
        
    def test_root_correct(self):
        self.assertAlmostEqual((7.0 ** 0.5) ** 2.0, 7.0)
        
``` 

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
        with self.assertRaises(ValueError):
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
        [f'{self.monkey.name} is {x}' for x in self.monkey.actions]
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


And the final version of tests for Monkey:


🪄 _<mark style="color:green;">Code:</mark>_

```python
class MonkeyTestCase(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        cls.monkey = Monkey('Foo', 3)
        
    @classmethod
    def tearDownClass(cls):
        del cls.monkey
        
    def test_naming(self):
        self.assertEqual(self.monkey.name, 'Foo')
        
    def test_aging(self):
        self.assertEqual(self.monkey.age, 3)
        
    def test_action(self):
        self.assertIn(
            self.monkey.action(),
            [f'{self.monkey.name} is {x}' for x in self.monkey.actions]
        )

suite = unittest.TestLoader().loadTestsFromModule(MonkeyTestCase())
unittest.TextTestRunner().run(suite)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
...
----------------------------------------------------------------------
Ran 3 tests in 0.007s
```
{% endcode %}

    
    OK





    <unittest.runner.TextTestResult run=3 errors=0 failures=0>



### Test suites

* Used to organize many tests
* Not used often, better use lib `pytest` or `nose`.
* Instead of unittest.main(), there are other ways to run the tests with a finer level of control, less terse output, and no requirement to be run from the command line. 

For example: 

```python
from unittest import TestLoader, TextTestRunner
suite = TestLoader().loadTestsFromTestCase(LordOfTheFails)
unittest.TextTestRunner(verbosity=2).run(suite)
```

## Tests structure

Even if it is very heavily project-dependent there are several general tests structures that differ by focusing particular entity in tests:
* OUT - Object Under Test
    * We testing particular object
* CUT - Class Under Test
    * We testing particular class
* MUT - Method Under Test
    * We testing particular method
* FUT - Function Under Test
    * We testing particular function

Our example above was testing a class - so was following "CUT" structure.

## Extended example

Let's enrich our code which we test (let's save and call this module as `monkey.py`):


```python
class Monkey:
    actions = ['saying "Boo boo boo"', "dancing rock&roll", "jumping like a crazy frog"]

    def __init__(self, name="Dummy Monkey", age=2, actions=None):
        self.name = name
        self.age = age
        if actions is not None:
            self.actions = actions

    def __str__(self):
        return f"Monkey '{self.name}' ({self.age} years old)"

    def action(self):
        from random import choice

        return f"{self.name} is {choice(self.actions)}"

    def set_name(self, new_name):
        if new_name:
            self.name = new_name

    def set_age(self, age):
        if age > 0:
            self.age = age

    def set_actions(self, actions):
        if isinstance(actions, (list, tuple)):
            self.actions = actions
```

Updated tests would be:


🪄 _<mark style="color:green;">Code:</mark>_

```python
import unittest

#from monkey import Monkey

class ExtendedMonkeyTestCase(unittest.TestCase):
    def setUp(self):
        self.default_name = "Dummy"
        self.new_name = "New One"
        self.default_age = 3
        self.new_age = 5
        self.default_actions = ['saying "Boo boo boo"', "sleeping", "eating"]
        self.new_actions = ["dreaming", "fighting", "eating"]
        self.monkey = Monkey(self.default_name, self.default_age, self.default_actions)

    def tearDown(self):
        del self.monkey

    def test_01_naming_default(self):
        self.assertEqual(self.monkey.name, self.default_name)

    def test_02_naming_new(self):
        self.monkey.set_name(self.new_name)
        self.assertEqual(self.monkey.name, self.new_name)

    def test_03_aging_default(self):
        self.assertEqual(self.monkey.age, self.default_age)

    def test_04_aging_new(self):
        self.monkey.set_age(self.new_age)
        self.assertEqual(self.monkey.age, self.new_age)

    @staticmethod
    def _get_all_possible_actions(monkey, actions):
        return [f"{monkey.name} is {x}" for x in actions]

    def test_05_action_default(self):
        self.assertIn(
            self.monkey.action(),
            self._get_all_possible_actions(self.monkey, self.default_actions),
        )

    def test_06_action_new(self):
        self.monkey.set_actions(self.new_actions)
        self.assertIn(
            self.monkey.action(),
            self._get_all_possible_actions(self.monkey, self.new_actions),
        )

suite = unittest.TestLoader().loadTestsFromModule(ExtendedMonkeyTestCase())
unittest.TextTestRunner().run(suite)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
......
----------------------------------------------------------------------
Ran 6 tests in 0.012s
```
{% endcode %}

    
    OK





    <unittest.runner.TextTestResult run=6 errors=0 failures=0>



## Test Case Example

Let's check "kind-of-real-world" example. It is of course mostly "mock" but still it is interesting project.

This would the contents of our `app.py` module with core logic of the program that will be tested:

```python
import random
import time

class Device:
    """
    Mock Device class
    """
    RESULT = "<{cmd}>: 200, OK"
    DATA = ["rtyu", "asd", "asdasdhh", "jfghghj"]

    def __init__(self, serial="0000"):
        self._serial = serial

    def _run_cmd(self, cmd, seconds=0):
        time.sleep(seconds)
        return self.RESULT.format(cmd=cmd)
        
    def start(self):
        return self._run_cmd("start")

    def reboot(self):
        return self._run_cmd("reboot")

    def pool_data(self):
        return self._run_cmd("pool", 3)

    def query(self, data=""):
        return f"RESULT is: {random.choice(self.DATA)}"
```

Let's write `BasicTestCase` which will be the basis of our actual test cases (let's assume that some `app.py` holds the main code being tested with core logic). 

Here in `BasicTestCase` we will store constants, define some basic stuff - fixtures:

```python
import unittest

from app import Device


class BasicTestCase(unittest.TestCase):
    SERIAL = "1111"
    START_SUCCESS_RESULT = "<start>: 200, OK"
    REBOOT_SUCCESS_RESULT = "<reboot>: 200, OK"
    POOL_DATA_SUCCESS_RESULT = "<pool>: 200, OK"
    QUERY_HEADER = "RESULT is: "
    TIME_LIMIT = 4

    @classmethod
    def setUpClass(cls):
        cls.device = Device(cls.SERIAL)
```

And our actual test would be:

```python
import unittest
import time

from tests.basic import BasicTestCase

class RunCommandsTests(BasicTestCase):
    def test_01_init(self):
        self.assertEqual(self.device.serial, self.SERIAL)
        
    def test_02_start(self):
        self.assertEqual(self.device.start(), self.START_SUCCESS_RESULT)
         
    def test_03_reboot(self):
        self.assertEqual(self.device.reboot(), self.REBOOT_SUCCESS_RESULT)

    def test_04_time_limit(self):
        start = time.time()
        result = self.device.pool_data()
        time_delta = time.time() - start

        self.assertLessEqual(time_delta, self.TIME_LIMIT, "Time limit is exceded")
        self.assertEqual(result, self.POOL_DATA_SUCCESS_RESULT)

    def test_05_query_non_empty(self):
        result = self.device.query()
        self.assertIn(self.QUERY_HEADER, result)
        self.assertGreater(len(result), len(self.QUERY_HEADER))
```

We can skip test:

```python
    @unittest.skip("This unit test is in progress...")
    def test_07_skip(self):
        # TODO: Need to update this:
        self.assertEqual(self.something(), self.that)
```

We can mark test as "Expected failure":

```python
    @unittest.expectedFailure
    def test_08_exp_fail(self):
        # The API is not ready yet...
        self.assertEqual(self.device.query("FUTURE CALL"), 42)
```