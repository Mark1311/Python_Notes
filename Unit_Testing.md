# Unit Testing

## What is Unit Testing?

Unit testing Python mein ek process hoti hai jisme aap apne code ke chhote-chhote hisson (functions ya methods) ko independently test karte hain. Iska main goal yeh hota hai ki aapke code ke har part ka behavior sahi ho aur jab aap code me koi changes karte hain, toh purana code bhi sahi tarike se kaam kare.

Python mein unit testing ko test cases likhkar kiya jaata hai, jisme aap specify karte hain ki aapke function se kis tarah ka output expect kiya jaa raha hai.

Test Case ==>  TestAddFunction ek test case hai jo unittest.TestCase class se inherit karta hai.

Assertions ==>  self.assertEqual() method ko use karte hue hum function ke result ko expected output ke saath compare karte hain.

Test Runner ==>  unittest.main() function tests ko run karta hai.

### Unit Testing ka Purpose:-

Unit testing ka main purpose yeh hai ki aap apne code ke har individual unit (jaise ki functions, methods, ya classes) ko independently test karein taaki aap ensure kar sakein ki har ek part sahi kaam kar raha hai. Agar koi bug ya error hota hai, toh usse bahut jaldi pakda jaa sakta hai, aur usse fix karna aasan ho jaata hai.

### Unit Test Ka Structure:

Test Case: Test case ek aisa code block hota hai jo ek particular functionality ko test karta hai.

Assertions: Assertions wo statements hote hain jo test karte hain ki aapka code expected results de raha hai ya nahi.

Test Suite: Test suite ek collection hoti hai test cases ki jo ek saath run ki jaati hai.

### Python mein unittest module:

Python mein unittest module ka use karke hum apne code ka unit testing kar sakte hain. Yeh module ek framework provide karta hai jo test cases likhne, test results ko evaluate karne, aur tests ko automate karne mein help karta hai.

### mportant Concepts:

#### Test Case: 

Ek test case wo method hoti hai jo ek specific functionality ko test karti hai. Jaise ki ek function ka output ya behavior.

#### Assertions: 
    
Assertions wo conditions hain jo aap test case mein likhte hain taaki check kar sakein ki function ka output expected value ke barabar hai ya nahi. Kuch common assertions yeh hain:

assertEqual(a, b) — Aap check karte hain ki a aur b ki value barabar honi chahiye.

assertTrue(x) — Aap check karte hain ki x ki value True honi chahiye.

assertFalse(x) — Aap check karte hain ki x ki value False honi chahiye.

assertRaises(exception, function, *args, **kwargs) — Aap check karte hain ki function call karne se exception raise ho raha hai ya nahi.

#### Test Suite: 

Test suite ek collection hoti hai test cases ki, jise ek saath execute kiya jaa sakta hai. Aap manually ya automatically test cases ko group kar sakte hain.


```python
import unittest

# Function to be tested
def multiply(a, b):
    return a * b

# Unit Test Class
class TestMultiplyFunction(unittest.TestCase):

    # Test Case 1: Multiply two positive numbers
    def test_multiply_positive(self):
        self.assertEqual(multiply(2, 3), 6)  # Expected result is 6

    # Test Case 2: Multiply a positive number and a negative number
    def test_multiply_negative(self):
        self.assertEqual(multiply(2, -3), -6)  # Expected result is -6

    # Test Case 3: Multiply a number with zero
    def test_multiply_zero(self):
        self.assertEqual(multiply(0, 5), 0)  # Expected result is 0

    # Test Case 4: Test that the function raises an exception for invalid input
    def test_multiply_invalid_input(self):
        with self.assertRaises(TypeError):  # Expecting TypeError if inputs are invalid
            multiply("string", 5)

# Run the test cases
if __name__ == "__main__":
    unittest.main()

```

Function to Test: Humne ek multiply function banaya hai jo do numbers ko multiply karta hai.

Test Case 1: test_multiply_positive mein humne do positive numbers ko multiply karke check kiya ki result sahi hai ya nahi.

Test Case 2: test_multiply_negative mein humne ek positive aur ek negative number ko multiply kiya.

Test Case 3: test_multiply_zero mein humne zero ke saath multiplication check kiya.

Test Case 4: test_multiply_invalid_input mein humne check kiya ki agar function ko invalid input diya jaye (jaise string aur integer ka combination), toh woh TypeError raise karega.

Test Runner: unittest.main() function tests ko run karta hai.

# Advantage of Unit Testing

1. Code ki Quality behtar hoti hai

2. Debugging asaan ho jaati hai

3.Refactoring mein madad milti hai

4. Documentation ki tarah kaam karta hai

5. Developer ka confidence barhta hai

6. Cost-effective hota hai

7. Continuous Integration (CI) mein madad

8. Code Design behtar hota hai

# DisAdvantage of UT?

1. Time and Effort

2. Dependence on Developers

3. Difficulty in Testing Complex Units

4. Difficulty in Testing Interactions

5. Difficulty in Testing User Interfaces

6. Over-reliance on Automation

7. Maintenance Overhead

# Assert Methods in Python Unittest

### assertEqual(a, b)
Checks if a == b


```python
self.assertEqual(2 + 2, 4)  # Passes
self.assertEqual(2 + 2, 5)  # Fails
```

### assertNotEqual(a, b)
Checks if a != b


```python
self.assertNotEqual(2 + 2, 5)  # Passes
self.assertNotEqual(2 + 2, 4)  # Fails
```

### assertTrue(x)
Checks if x is true


```python
self.assertTrue(1 == 1)  # Passes
self.assertTrue(1 == 2)  # Fails
```

### assertFalse(x)
Checks if x is false.


```python
self.assertFalse(1 == 2)  # Passes
self.assertFalse(1 == 1)  # Fails
```

### assertIs(a, b)
Checks if a is b (using is)


```python
self.assertIs(None, None)  # Passes
self.assertIs(2, 2)  # Fails, because they are not the same object
```

### assertIsNot(a, b)
Checks if a is not b (using is not).


```python
self.assertIsNot(None, 2)  # Passes
self.assertIsNot(2, 2)  # Fails
```

### assertIsNone(x)
Checks if x is None.


```python
self.assertIsNone(None)  # Passes
self.assertIsNone(1)  # Fails
```

### assertIsNotNone(x)
Checks if x is not None.


```python
self.assertIsNotNone(1)  # Passes
self.assertIsNotNone(None)  # Fails
```

### assertIn(a, b)
Checks if a is in b.
Fails if a is not in b.


```python
self.assertIn(3, [1, 2, 3])  # Passes
self.assertIn(4, [1, 2, 3])  # Fails
```

### assertNotIn(a, b)
Checks if a is not in b.
Fails if a is in b.


```python
self.assertNotIn(4, [1, 2, 3])  # Passes
self.assertNotIn(3, [1, 2, 3])  # Fails
```

### assertIsInstance(a, b)
Checks if a is an instance of class b.
Fails if a is not an instance of b.


```python
self.assertIsInstance(5, int)  # Passes
self.assertIsInstance(5, str)  # Fails
```

### assertNotIsInstance(a, b)
Checks if a is not an instance of class b.
Fails if a is an instance of b.


```python
self.assertNotIsInstance(5, str)  # Passes
self.assertNotIsInstance(5, int)  # Fails
```

### assertGreater(a, b)
Checks if a > b.
Fails if a is not greater than b


```python
self.assertGreater(5, 3)  # Passes
self.assertGreater(3, 5)  # Fails
```

### assertGreaterEqual(a, b)
Checks if a >= b.
Fails if a is less than b.


```python
self.assertGreaterEqual(5, 3)  # Passes
self.assertGreaterEqual(3, 5)  # Fails
```

### assertLess(a, b)
Checks if a < b.
Fails if a is not less than b.


```python
self.assertLess(3, 5)  # Passes
self.assertLess(5, 3)  # Fails
```

### assertLessEqual(a, b)
Checks if a <= b.
Fails if a is greater than b.


```python
self.assertLessEqual(3, 5)  # Passes
self.assertLessEqual(5, 3)  # Fails
```


```python
# Example:--->

import unittest

class TestMathOperations(unittest.TestCase):

    def test_addition(self):
        self.assertEqual(2 + 2, 4)
        self.assertNotEqual(2 + 2, 5)
        self.assertTrue(2 + 2 == 4)
        self.assertFalse(2 + 2 == 5)

if __name__ == '__main__':
    unittest.main()

```

# Write a unit test for a simple method that checks if a number is prime.


```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True
```


```python
import unittest

class TestPrimeMethod(unittest.TestCase):
    
    def test_prime_numbers(self):
        # Test some known prime numbers
        self.assertTrue(is_prime(2))
        self.assertTrue(is_prime(3))
        self.assertTrue(is_prime(5))
        self.assertTrue(is_prime(7))
        self.assertTrue(is_prime(11))
        
    def test_non_prime_numbers(self):
        # Test non-prime numbers
        self.assertFalse(is_prime(1))
        self.assertFalse(is_prime(4))
        self.assertFalse(is_prime(6))
        self.assertFalse(is_prime(8))
        self.assertFalse(is_prime(9))
        
    def test_large_prime_number(self):
        # Test a large prime number
        self.assertTrue(is_prime(997))

    def test_large_non_prime_number(self):
        # Test a large non-prime number
        self.assertFalse(is_prime(1000000))

if __name__ == "__main__":
    unittest.main()
```


```python

```
