---
sidebar_position 1
---

# Cheat Sheet

## Basic Structure

```python
import unittest

class TestMyFunction(unittest.TestCase)
    def test_case1(self)
        # Test goes here
        self.assertEqual(function_to_test(arguments), expected_result)
```

## Running Tests

**Command Line**

```
python m unittest discover
```

**Specific Module**

```
python m unittest test_module.py
```

**Within a Python Script**

```python
if __name__ == '__main__'
    unittest.main()
```

## Assertions

**Equality**

```python
self.assertEqual(a, b)
self.assertNotEqual(a, b)
```

**Truthiness**

```python
self.assertTrue(x)
self.assertFalse(x)
```

**Identity**

```python
self.assertIs(a, b)
self.assertIsNot(a, b)
```

**Containers**

```python
self.assertIn(item, container)
self.assertNotIn(item, container)
```

**Exceptions**

```python
with self.assertRaises(SomeException)
    function_that_raises()
```

## Setup and Teardown

**Method Level**

```python
def setUp(self)
    # Code to run before each test method
def tearDown(self)
    # Code to run after each test method
```

**Class Level**

```python
@classmethod
def setUpClass(cls)
    # Code to run once before all tests in the class
@classmethod
def tearDownClass(cls)
    # Code to run once after all tests in the class
```

## Skipping Tests

**Skipping a Test**

```python
@unittest.skip("Reason for skipping")
def test_something(self)
    # Test code here
```

**Conditional Skipping**

```python
@unittest.skipIf(condition, "Reason for skipping")
def test_something(self)
    # Test code here
```

## Mocking with `unittest.mock`

**Basic Mock**

```python
from unittest.mock import Mock
mock_obj = Mock(return_value='fake response')
result = mock_obj('arg')
mock_obj.assert_called_once_with('arg')
```

**Patch Function**

```python
from unittest.mock import patch

@patch('module.ClassName')
def test_method(self, mock_class)
    instance = mock_class.return_value
    instance.method.return_value = 'mocked response'
    # Test using instance.method()
    instance.method.assert_called_once()
```

**Mock Side Effects**

```python
mock_obj = Mock(side_effect=[ValueError, 'fake response'])
# First call raises ValueError, second call returns 'fake response'
```

### Testing Exceptions

```python
with self.assertRaises(ValueError)
    function_that_raises_value_error()
```

## Testing with Assertions

**Asserting a List of Calls**

```python
mock_obj.method.call_args_list == [call('first_call'), call('second_call')]
```

## Using Test Suites

```python
def suite()
    suite = unittest.TestSuite()
    suite.addTest(TestMyFunction('test_case1'))
    suite.addTest(TestAnotherFunction('test_case2'))
    return suite

if __name__ == '__main__'
    runner = unittest.TextTestRunner()
    runner.run(suite())
```

## Parameterized Tests

While `unittest` does not natively support parameterized tests, you can achieve this functionality using a combination of test generation techniques or thirdparty libraries like `parameterized`.

```python
from parameterized import parameterized

class TestMathOperation(unittest.TestCase)
    @parameterized.expand([
        (2, 3, 5),
        (4, 5, 9),
        (1, 1, 0),
    ])
    def test_addition(self, a, b, expected)
        self.assertEqual(a + b, expected)
```

This cheat sheet provides a quick overview of the most commonly used features and best practices for Python's `unittest` framework, including writing and organizing tests, using assertions, setting up and tearing down test environments, skipping tests, and mocking dependencies. For more detailed information and advanced features, refer to the official `unittest` documentation.
