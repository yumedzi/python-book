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


```python
import unittest

class TestStringMethods(unittest.TestCase):
    def test_01_upper(self):
        self.assertEqual('fooooool000'.lower(), 'FOOOOOO1000'.lower(), "Critical Python string handling error")

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

    F..
    ======================================================================
    FAIL: test_01_upper (__main__.TestStringMethods)
    ----------------------------------------------------------------------
    Traceback (most recent call last):
      File "<ipython-input-12-af5344e748c5>", line 5, in test_01_upper
        self.assertEqual('fooooool000'.lower(), 'FOOOOOO1000'.lower(), "Critical Python string handling error")
    AssertionError: 'fooooool000' != 'foooooo1000'
    - fooooool000
    ?        ^
    + foooooo1000
    ?        ^
     : Critical Python string handling error
    
    ----------------------------------------------------------------------
    Ran 3 tests in 0.009s
    
    FAILED (failures=1)


Result:

```
$ python super_script.py -v
test (__main__.SomeTest) ... ok