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
* test suite
    * A test suite is a collection of test cases, test fixtures, or both.
* test runner
    * A test runner is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.


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


```python
import unittest

class TestStringMethods(unittest.TestCase):
    def test_01_upper(self):
        self.assertEqual('fooooool000'.upper(), 'FOOOOOO1000', "Critical Python string handling error")

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
      File "<ipython-input-6-3628783ca985>", line 5, in test_01_upper
        self.assertEqual('fooooool000'.upper(), 'FOOOOOO1000', "Critical Python string handling error")
    AssertionError: 'FOOOOOOL000' != 'FOOOOOO1000'
    - FOOOOOOL000
    ?        ^
    + FOOOOOO1000
    ?        ^
     : Critical Python string handling error
    
    ----------------------------------------------------------------------
    Ran 3 tests in 0.006s
    
    FAILED (failures=1)


Result:
    
```shell
$ python super_script.py -v
test (__main__.SomeTest) ... ok