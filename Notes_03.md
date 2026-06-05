# What are Python’s key features?

* Simple and Readable Syntax

* Interpreted

* Dynamically Typed

* Multi-Paradigm

* Extensive Standard Library

* Cross-Platform

* High-Level

* Open Source

* Large Ecosystem

* Community Support

* Embeddable and Extensible

# What is the difference between is and ==?


### 🔹 == (Equality Operator)

`== check karta hai values same hain ya nahi.`

* Agar do objects ki value equal hai, to == → True return karega
* Chahe ye objects alag memory location par ho.


```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)  # True (values same)
```

### 🔹 is (Identity Operator)

`is check karta hai kya dono variables ek hi memory location ko point kar rahe hain.`


```python
a = [1, 2, 3]
b = a
print(a is b)  # True (same object)
#------------------------------------------------------#
a = [1, 2, 3]
b = [1, 2, 3]
print(a is b)  # False (same memory nahi
```

    True
    False
    

### Behavior with Immutable Types

For immutable types (like integers, strings), is may return True for objects with the same value due to Python's internal caching.


```python
a = 1000
b = 1000
print(a == b)  # True (values are equal)
print(a is b)  # False (different objects, no caching for large integers)

x = 10
y = 10
print(x == y)  # True (values are equal)
print(x is y)  # True (small integers are cached)
```


```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)  # True (same value)
print(a is b)  # False (different objects)
#--------------------------------------------------
x = 5
y = 5
print(x == y)  # True
print(x is y)  # True (integers cache hone ki wajah se same memory use hoti)
```

##### What Are Immutable Types?

Immutable types are objects whose value cannot be changed after creation. Examples include:

* Integers (int)

* Strings (str)

* Tuples (tuple)

#### How is Works with Immutable Types


* Python internally optimizes memory usage for immutable objects by reusing objects with the same value in some cases.

* This optimization is called object interning.

##### Small Immutable Objects (e.g., Small Integers, Short Strings)

* Python caches small integers (commonly from -5 to 256) and short strings for performance reasons.

* If two variables are assigned the same small integer or string, they point to the same memory location.


```python
a = 10
b = 10
print(a is b)  # True (10 is cached)

x = "hello"
y = "hello"
print(x is y)  # True (short strings are cached)
```

###### Large Immutable Objects

* For larger integers and longer strings, Python does not guarantee caching. New objects are created in memory.


```python
a = 1000
b = 1000
print(a is b)  # False (different objects in memory)

x = "a very long string"
y = "a very long string"
print(x is y)  # False (no caching for long strings)

```

    False
    False
    

##### Why This Happens?

* Caching small values avoids repeatedly creating new objects, which saves memory and improves performance.

* For larger or more complex objects, Python creates separate objects to avoid unnecessary overhead.



##### Key Takeaway

* For small immutable objects like integers in the range -5 to 256 and short strings, is may return True because Python reuses them.

* For large immutable objects, is usually returns False because Python creates new objects even if their values are the same.

# What are Python's mutable and immutable data types?


#### Immutable Data Types

* Numbers: int, float, complex

* Strings: str

* Tuples: tuple

* Frozen Sets: frozenset

* Booleans: bool

#### Mutable Data Types

* Lists: list

* Dictionaries: dict

* Sets: set

* Byte Arrays: bytearray

| **Aspect**          | **Mutable**                  | **Immutable**         |
| ------------------- | ---------------------------- | --------------------- |
| **Modification**    | Allowed                      | Not allowed           |
| **Memory Behavior** | Modifies the existing object | Creates a new object  |
| **Examples**        | `list`, `dict`, `set`        | `int`, `str`, `tuple` |


# What are Python's built-in data structures?

| **Data Structure** | **Mutable** | **Allows Duplicates** | **Ordered** |
| ------------------ | ----------- | --------------------- | ----------- |
| **List**           | Yes         | Yes                   | Yes         |
| **Tuple**          | No          | Yes                   | Yes         |
| **Dictionary**     | Yes         | Keys: No, Values: Yes | No          |
| **Set**            | Yes         | No                    | No          |
| **Frozenset**      | No          | No                    | No          |
| **String**         | No          | Yes                   | Yes         |



```python
my_frozenset = frozenset([1, 2, 3])
```

# What is the use of self in Python classes?


Python me self ek convention hai jo kisi class ke instance (object) ko refer karta hai. Ye class ke methods aur properties ko access karne aur manage karne ke liye use hota hai, har object ke liye alag-alag.

`1. Instance variables ko access karne ke liye.`

self ka use class ke andar variables (attributes) ko instance-specific banane ke liye hota hai.


```python
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age

    def show_details(self):
        print(f"Name: {self.name}, Age: {self.age}")

person1 = Person("Ravi", 25)
person2 = Person("Anita", 30)

person1.show_details()  # Output: Name: Ravi, Age: 25
person2.show_details()  # Output: Name: Anita, Age: 30

```

`2. Methods ko call karne ke liye.`

Aap ek method se doosre method ko self ke through call kar sakte ho.


```python
class Calculator:
    def add(self, a, b):
        return a + b

    def multiply(self, a, b):
        return self.add(a, b) * 2  # add() method ko call kiya

calc = Calculator()
print(calc.multiply(3, 5))  # Output: 16

```

Kyun zaroori hai self?

* Python ko yeh batane ke liye ki kis object ke saath kaam ho raha hai.

* Har object ki unique identity banaye rakhne ke liye.

* Class ke andar instance variables aur methods ko access karne ka standard way hai.

Important Notes:

* self ek convention hai, iska naam kuch aur bhi ho sakta hai, lekin readability ke liye self use karna best practice hai.

* Static methods aur class methods me self ki zarurat nahi hoti.

# Write a function to count the number of vowels in a string.



```python
def count_vowels(input_string):

    vowels = "aeiouAEIOU"  # List of vowels (both lowercase and uppercase)
    count = 0
    for char in input_string:
        if char in vowels:
            count += 1
    return count

# Example usage
example_string = "Hello, how many vowels are there?"
print(f"Number of vowels: {count_vowels(example_string)}")
```

    Number of vowels: 10
    

# Class, Instance and Object

## 1. Class

`Definition:`

* Class ek blueprint ya template hota hai jo objects banane ke liye use hota hai.
* Isme attributes (data) aur methods (functions) define kiye jaate hain jo objects use karte hain.

Key Point:

* Class sirf ek idea ya definition hai, real-world entity nahi hai.


```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

# Yahaan Car ek class hai jo define karti hai ki cars ke paas brand aur color hoga.

```

## 2. Object

`Definition:`

* Object ek real-world entity hai jo class ke template ke according banti hai.
* Class ke attributes aur methods ka real implementation hota hai object.

Key Point:

* Objects ek class ke instance hote hain. Ek class se multiple objects ban sakte hain.


```python
car1 = Car("Toyota", "Red")  # Object 1
car2 = Car("Honda", "Blue")  # Object 2

# Yahaan car1 aur car2 objects hain jo Car class ka real-world implementation hain.
```

## 3. Instance

`Definition:`

* Instance ek specific object hota hai jo kisi particular class ka hai. Object aur instance kaafi similar hain, lekin instance ka reference specific class ke saath hota hai.

Key Point:

* Instance ka matlab hota hai "ye object kis class ka hai". Har object ek instance hota hai, lekin instance word generally class ke context me use hota hai.


```python
print(isinstance(car1, Car))  # Output: True

# Yahaan car1 ek instance hai Car class ka.
```

| **Aspect**     | **Class**                          | **Object**                                  | **Instance**                     |
| -------------- | ---------------------------------- | ------------------------------------------- | -------------------------------- |
| **Definition** | Blueprint ya template for objects. | Real-world implementation of class.         | Specific object of a class.      |
| **Memory**     | Memory allocate nahi hoti.         | Memory allocate hoti hai.                   | Memory allocate hoti hai.        |
| **Relation**   | Objects ko define karta hai.       | Ek class ke multiple objects ho sakte hain. | Har object ek instance hota hai. |
| **Example**    | `Car`                              | `car1 = Car("Toyota", "Red")`               | `car1` is an instance of `Car`.  |


# What is the difference between a list and a tuple?


| **Feature**      | **List**                      | **Tuple**                        |
| ---------------- | ----------------------------- | -------------------------------- |
| **Mutability**   | Mutable                       | Immutable                        |
| **Syntax**       | Square brackets `[ ]`         | Parentheses `( )`                |
| **Performance**  | Slower                        | Faster                           |
| **Memory Usage** | More                          | Less                             |
| **Functions**    | Many (e.g., `append`, `sort`) | Limited (e.g., `count`, `index`) |
| **Use Case**     | Dynamic data                  | Fixed data                       |


# How do you remove duplicates from a list?



```python
# List with duplicates
my_list = [1, 2, 2, 3, 4, 4, 5]

# Removing duplicates while preserving order
unique_list = []
for item in my_list:
    if item not in unique_list:
        unique_list.append(item)

print(unique_list)  # Output: [1, 2, 3, 4, 5]

```


```python
# List with duplicates
my_list = [1, 2, 2, 3, 4, 4, 5]

# Removing duplicates
unique_list = list(set(my_list))

print(unique_list)  # Output: [1, 2, 3, 4, 5]

```

# Reverse a string in Python.



```python
# Original string
my_string = "Hello"

# Reversing the string
reversed_string = my_string[::-1]

print(reversed_string)  # Output: "olleH"

```


```python
# Original string
my_string = "Hello"

# Reversing the string using a loop
reversed_string = ""
for char in my_string:
    reversed_string = char + reversed_string

print(reversed_string)  # Output: "olleH"

```


```python
# Function to reverse a string (Using Recursive)
def reverse_string(s):
    if len(s) == 0:
        return s
    return reverse_string(s[1:]) + s[0]

# Original string
my_string = "Hello"

# Reversing the string
reversed_string = reverse_string(my_string)

print(reversed_string)  # Output: "olleH"

```


```python
# Original string
my_string = "Hello"

# Reversing the string using reversed()
reversed_string = ''.join(reversed(my_string))

print(reversed_string)  # Output: "olleH"

```

| **Method**          | **Simplicity** | **Performance**       | **Recommended Use Case**                 |
| ------------------- | -------------- | --------------------- | ---------------------------------------- |
| Slicing `[::-1]`    | Very simple    | Very fast             | Best for quick reversals                 |
| Loop                | Moderate       | Slower                | If customization is required             |
| `reversed()` + join | Simple         | Fast                  | When handling iterables or strings       |
| Recursion           | Complex        | Slow (stack overhead) | For learning or conceptual understanding |


# Check if a number is a palindrome.



```python
def is_palindrome(num):
    # Convert number to string
    num_str = str(num)
    # Check if the string is equal to its reverse
    return num_str == num_str[::-1]

# Test the function
print(is_palindrome(121))  # Output: True
print(is_palindrome(123))  # Output: False

```


```python
def is_palindrome(num):
    # Negative numbers are not palindromes
    if num < 0:
        return False
    
    original = num
    reversed_num = 0

    # Reverse the number
    while num > 0:
        digit = num % 10  # Extract the last digit
        reversed_num = reversed_num * 10 + digit  # Build the reversed number
        num //= 10  # Remove the last digit
    
    # Check if original number is equal to reversed number
    return original == reversed_num

# Test the function
print(is_palindrome(121))  # Output: True
print(is_palindrome(-121))  # Output: False
print(is_palindrome(123))  # Output: False

```


```python
def reverse_number(num, reversed_num=0):
    if num == 0:
        return reversed_num
    return reverse_number(num // 10, reversed_num * 10 + num % 10)

def is_palindrome(num):
    if num < 0:
        return False
    return num == reverse_number(num)

# Test the function
print(is_palindrome(121))  # Output: True
print(is_palindrome(123))  # Output: False

```

| **Method**         | **Converts to String** | **Performance** | **Use Case**                 |
| ------------------ | ---------------------- | --------------- | ---------------------------- |
| Convert to String  | Yes                    | Fast            | Simple and quick solution    |
| Without Conversion | No                     | Efficient       | For pure mathematical checks |
| Using Recursion    | No                     | Slower          | For conceptual understanding |


# Find the factorial of a number using recursion.



```python
def factorial(n):
    if n < 0:
        return "Factorial is not defined for negative numbers."
    if n == 0:
        return 1
    return n * factorial(n - 1)

```

# Find the second largest number in a list.



```python
def second_largest(numbers):
    if len(numbers) < 2:
        return "Second largest does not exist."

    largest = second = float('-inf')  # Initialize with negative infinity

    for num in numbers:
        if num > largest:
            second = largest
            largest = num
        elif num > second and num != largest:
            second = num

    return second if second != float('-inf') else "Second largest does not exist."

# Test the function
print(second_largest([4, 1, 3, 4, 2]))  # Output: 3
print(second_largest([10, 10, 10]))     # Output: "Second largest does not exist."

```


```python
def second_largest(numbers):
    unique_numbers = list(set(numbers))  # Remove duplicates
    if len(unique_numbers) < 2:
        return "Second largest does not exist."
    unique_numbers.sort(reverse=True)  # Sort in descending order
    return unique_numbers[1]  # Return the second largest element

# Test the function
print(second_largest([4, 1, 3, 4, 2]))  # Output: 3
print(second_largest([10, 10, 10]))     # Output: "Second largest does not exist."

```

# What does it mean for code to be “Pythonic”? Give an example.


"Pythonic" ka matlab hai Python ki idioms, conventions, aur best practices ka use karke code likhna jo readable, concise, aur elegant ho. Pythonic code Python language ke unique features ka maximum advantage uthata hai aur unnecessarily complex ya verbose nahi hota.

* Clarity: Code samajhne aur maintain karne me easy ho.

* Simplicity: Unnecessary complexity ko avoid karna.

* Efficiency: Python ke built-in functions aur idioms ka use.

The Zen of Python

Pythonic code likhne ke liye, "The Zen of Python" ke kuch important principles yaad rakhein. (Run import this in Python to see them.)

Why Is Writing Pythonic Code Important?

* Better Readability: Dusre developers code ko asaani se samajh sakte hain.

* Maintainability: Code ko modify karna aur debug karna easy hota hai.

* Performance: Python ke built-in functions aur idioms ka use karke code efficient hota hai.

* Community Standards: Python developers Pythonic code likhne ki expectation rakhte hain, jo collaboration me helpful hota hai.

# What Are Lambda Functions?


Lambda functions Python me anonymous (nameless) functions hain jo ek single expression ko define karte hain. Inhe inline functions bhi kaha jata hai, kyunki ye ek hi line me likhe jate hain aur kisi ek short-lived kaam ke liye use hote hain.

`lambda:` Keyword to define a lambda function.

`arguments:` Input parameters (optional).

`expression:` Ek single expression jo evaluate hota hai aur return karta hai.


```python
lambda arguments: expression
```

### Regular function


```python
def add(x, y):
    return x + y
```

### Lambda function


```python
add_lambda = lambda x, y: x + y
print(add_lambda(3, 5))  # Output: 8
```

## Example:-


```python

add = lambda a, b: a + b
print(add(5, 3))   # Output → 8

#-------------------------------

numbers = [1, 2, 3, 4, 5, 6]
even = list(filter(lambda x: x % 2 == 0, numbers))

print(even)   # Output → [2, 4, 6]

#-------------------------------------------

students = [("Ravi", 20), ("Aman", 18), ("Sita", 22)]

sorted_data = sorted(students, key=lambda x: x[1])

print(sorted_data)
# Output → [('Aman', 18), ('Ravi', 20), ('Sita', 22)]

#---------------------------------------------------

numbers = [1, 2, 3, 4]
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # Output: [1, 4, 9, 16]

```

| Feature         | Lambda Function                 | Regular Function (`def`)   |
| --------------- | ------------------------------- | -------------------------- |
| **Syntax**      | `lambda x: x + 2`               | `def add(x): return x + 2` |
| **Name**        | Nameless (anonymous)            | Requires a name            |
| **Use Case**    | Short-lived, quick operations   | Complex, reusable logic    |
| **Readability** | Less readable for complex logic | More readable and explicit |


# Explain list comprehensions and dictionary comprehensions with examples.


#### List Comprehension


```python
# Syntax

[expression for item in iterable if condition]
```


```python
squares = [x**2 for x in range(5)]
print(squares)  # Output: [0, 1, 4, 9, 16]
```


```python
numbers = [1, 2, 3, 4, 5, 6]
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # Output: [2, 4, 6]
```


```python
numbers = [1, 2, 3, 4, 5, 6]
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # Output: [2, 4, 6]
```

#### Dictionary Comprehension


```python
# Syntax

{key_expression: value_expression for item in iterable if condition}
```


```python
squares_dict = {x: x**2 for x in range(5)}
print(squares_dict)  # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```


```python
numbers = [1, 2, 3, 4, 5]
even_squares = {x: x**2 for x in numbers if x % 2 == 0}
print(even_squares)  # Output: {2: 4, 4: 16}
```


```python
original = {'a': 1, 'b': 2, 'c': 3}
reversed_dict = {v: k for k, v in original.items()}
print(reversed_dict)  # Output: {1: 'a', 2: 'b', 3: 'c'}
```

| Feature            | List Comprehension         | Dictionary Comprehension      |
| ------------------ | -------------------------- | ----------------------------- |
| **Output Type**    | List                       | Dictionary                    |
| **Syntax Example** | `[x**2 for x in range(5)]` | `{x: x**2 for x in range(5)}` |
| **Use Cases**      | Sequential data            | Key-value mappings            |


# What are class methods and static methods?

#### Class Methods (@classmethod)

Definition:

* Class methods ko class ke context me kaam karne ke liye design kiya gaya hai, na ki kisi specific object (instance) ke liye.

* Ye class-level variables ko access kar sakte hain aur modify kar sakte hain.

* Class methods me cls argument hota hai, jo class ko represent karta hai (similar to self for instance methods).

Kaise Banate Hain?

`@classmethod decorator ka use karke define kiya jata hai.`


```python
class MyClass:
    class_variable = 0  # Class-level variable

    @classmethod
    def set_class_variable(cls, value):
        cls.class_variable = value  # Modify class-level variable

    @classmethod
    def get_class_variable(cls):
        return cls.class_variable  # Access class-level variable

# Test class method
MyClass.set_class_variable(10)
print(MyClass.get_class_variable())  # Output: 10

```


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, birth_year):
        return cls(name, 2023 - birth_year)

# Create a Person object using a class method
person = Person.from_birth_year("Alice", 1995)
print(person.name, person.age)  # Output: Alice 28

```

#### Static Methods (@staticmethod)

Definition:

* Static methods ko class ya instance ke context ki zarurat nahi hoti.

* Ye utility functions ki tarah kaam karte hain, jo class ke andar logically belong karte hain.

* Inme self ya cls argument nahi hota.

Kaise Banate Hain?

`@staticmethod decorator ka use karke define kiya jata hai.`


```python
class Calculator:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def multiply(a, b):
        return a * b

# Test static methods
print(Calculator.add(5, 3))       # Output: 8
print(Calculator.multiply(5, 3))  # Output: 15

```

| **Feature**              | **Class Method**                      | **Static Method**                    |
| ------------------------ | ------------------------------------- | ------------------------------------ |
| **Decorator**            | `@classmethod`                        | `@staticmethod`                      |
| **Takes `cls/self`?**    | Takes `cls` as first argument         | Does not take `self` or `cls`        |
| **Access to Class Data** | Can access and modify class variables | Cannot access class or instance data |
| **Use Case**             | Operates on class-level data          | General utility or helper functions  |


##### Class Method:

* @classmethod decorator use hota hai.

* cls argument leta hai, jo class ko represent karta hai.

* Class-level data ko access aur modify karne ke liye use hota hai.

##### Static Method:

* @staticmethod decorator use hota hai.

* Class ya instance ke context ki zarurat nahi hoti.

* Utility functions ke liye use hota hai.

| Feature / Point               | **Class Method**                                       | **Static Method**                               |
| ----------------------------- | ------------------------------------------------------ | ----------------------------------------------- |
| Definition                    | `@classmethod` decorator se banता                      | `@staticmethod` decorator se बनता               |
| First argument                | `cls` leta (class ko refer karta)                      | Koi default argument nahi (na `self`, na `cls`) |
| Kis par operate karta         | **Class** par (class variables use/modify kar सकता है) | Class ya object se **koi lena dena nahi**       |
| Object ki need                | Object banane ki zarurat nahi                          | Object banane ki zarurat nahi                   |
| Typical use                   | Factory methods, class-level data ko modify karna      | Utility/helper functions                        |
| Can access class variables    | ✔️ Yes                                                 | ❌ No (jab tak manually pass na karo)            |
| Can access instance variables | ❌ No                                                   | ❌ No                                            |
| Call kaise hota               | Class ya object dono se                                | Class ya object dono se                         |
| Bound to                      | Class                                                  | Function                                        |


# ____init____.py File in Python Kya Hota Hai?


__init__.py ek special file hai jo Python me ek directory ko package banata hai. Is file ki wajah se Python samajhta hai ki jis folder me ye file hai, usse ek package ki tarah treat karna chahiye.

#### Purpose of __init__.py

1. Package Ko Identify Karna:

* Jab ek folder me __init__.py file hoti hai, to Python interpreter us folder ko ek package ke roop me recognize karta hai.

* Python 3.3 ke baad __init__.py file mandatory nahi hai, par isse best practice ke roop me rakha jata hai.

2. Package Initialization:

* Jab aap ek package ko import karte ho, __init__.py file automatically execute hoti hai.

* Ye file package ke initialization tasks ko handle kar sakti hai (e.g., dependencies load karna, variables define karna).

3. Module Import Simplify Karna:

* __init__.py ka use karke aap package ke andar modules aur sub-packages ko import aur organize kar sakte ho.

##### Key Points

* Python 3.3 se pehle: __init__.py file har package me hona zaroori tha.
* 
* Python 3.3 ke baad: Ye optional ho gaya, par still best practice hai.
* 
* Initialization Tasks: Dependencies load karna, configuration set karna.
* 
* Simplifies Imports: Modular structure maintain karne me madad karta hai.

# What is the difference between an iterator and an iterable?


Python me iterator aur iterable donon ek tarike se data ko traverse karne ke concepts hain. Ye loops aur sequential data processing ke liye kaafi useful hote hain. In dono ke beech farq samajhne ke liye niche ka explanation dekhein:

### Iterable

Definition:

* Iterable ek aisa object hota hai jo elements ka collection hota hai (jaise list, tuple, string, etc.) aur jisko hum ek-ek karke traverse kar sakte hain.

* Ye __iter__() method implement karta hai, jo ek iterator object return karta hai.


```python
# Examples of iterable objects
my_list = [1, 2, 3]       # List
my_string = "hello"       # String
my_tuple = (4, 5, 6)      # Tuple
```


```python
for item in my_list:
    print(item)
# Output:
# 1
# 2
# 3
```

### Iterator

Definition:

* Iterator ek aisa object hota hai jo ek iterable se create hota hai aur __next__() method ko implement karta hai.

* Ye ek stateful object hota hai jo iterable ke elements ko ek-ek karke traverse karta hai.

Characteristics:

* Iterator object __iter__() aur __next__() methods ko implement karta hai.

* Jab __next__() method call hota hai, to iterator next element return karta hai.

* Jab elements khatam ho jate hain, StopIteration exception raise hoti hai.

##### Creating an Iterator

Using iter():

Iterable ko iterator me convert karne ke liye hum iter() function ka use karte hain.


```python
my_list = [1, 2, 3]
my_iterator = iter(my_list)

print(next(my_iterator))  # Output: 1
print(next(my_iterator))  # Output: 2
print(next(my_iterator))  # Output: 3
# StopIteration error if called again
```

| **Feature**           | **Iterable**                         | **Iterator**                          |
| --------------------- | ------------------------------------ | ------------------------------------- |
| **Definition**        | Collection of elements               | Object to traverse elements           |
| **Implements**        | `__iter__()` method                  | `__iter__()` and `__next__()` methods |
| **Examples**          | Lists, Tuples, Strings, Dictionaries | Object returned by `iter()` function  |
| **Use in Loops**      | Directly usable in loops             | Requires manual `next()` call         |
| **State Maintenance** | No                                   | Yes                                   |


### Summary

#### Iterable:

* Aise objects jo traversable hain, jaise list, string, tuple.

* Inke paas __iter__() method hota hai jo ek iterator return karta hai.

* for loop ke liye directly use karte hain.

#### Iterator:

* Ye iterable se bana hua object hai jo sequentially elements ko traverse karta hai.

* Inke paas __iter__() aur __next__() methods hote hain.

* next() function se ek element return karta hai, jab tak StopIteration raise na ho.

# What is the difference between __str__() and __repr__()?


Python me __str__() aur __repr__() dono special methods hain jo kisi object ko string ke form me represent karte hain. Inka main purpose ek object ka human-readable ya developer-readable representation provide karna hota hai.

### 1. __str__()

Purpose:

* __str__() ka use hota hai ek object ka human-friendly representation dene ke liye.

* Ye method tab call hota hai jab aap print(object) ya str(object) call karte ho.

Focus:

* Readable aur user-friendly information dena.


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Person(name={self.name}, age={self.age})"

person = Person("Alice", 30)
print(person)  # Output: Person(name=Alice, age=30)

```

### 2. __repr__()

Purpose:

* __repr__() ka use hota hai ek object ka developer-friendly representation dene ke liye.

* Ye method tab call hota hai jab aap repr(object) ya interactive Python shell me object ko directly print karte ho.

* Ye representation ideally aise hona chahiye ki object ko reconstruct karne ke liye use ho sake.

Focus:

* Debugging aur development ke liye detailed information dena.


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

person = Person("Alice", 30)
print(repr(person))  # Output: Person('Alice', 30)

```

| Point           | `str()`                                        | `repr()`                                                    |
| --------------- | ---------------------------------------------- | ----------------------------------------------------------- |
| Purpose         | User ko readable output dena                   | Developer ko debugging / correct object representation dena |
| Output Style    | Simple, clean, friendly                        | Exact, technical, raw (object reproduce ho sake)            |
| Used By         | `print()` and `str()`                          | `repr()` or Python shell                                    |
| Target Audience | End users                                      | Developers                                                  |
| Focus           | Readability                                    | Accuracy                                                    |
| Fallback        | Agar `__str__()` na ho → `__repr__()` use hota | Agar `__repr__()` na ho → object ka memory address          |
| Best Use Case   | Screen par output dikhana                      | Debugging, logging, object ka real structure dekhna         |



```python
## Example

text = "Hello\nWorld"

print(str(text))   # str() version

#Output:-   Hello
            World

print(repr(text))  # repr() version

#Output:- 'Hello\nWorld'

```

#### When to Use Which?

##### __str__():

* Jab aapko end-user ke liye output banana ho.

* Simple aur readable representation dena ho.

##### __repr__():

* Jab aapko object ka debugging aur development ke liye detailed output banana ho.

* Object ko reconstruct karne ke liye ek valid Python expression chahiye ho.

# Explain the concept of Python’s memory management.


Python ka memory management ek automatic process hai jo aapke program ke liye memory allocate aur deallocate karta hai. Ye process Python interpreter ke Memory Manager aur Garbage Collector ke through hota hai. Iska main purpose efficient memory usage ensure karna aur unused memory ko free karna hai.

### Python Objects and Memory Allocation

* Python me sab kuch ek object hai (numbers, strings, functions, etc.).

* Jab aap ek variable banate ho, Python uske liye memory allocate karta hai.

* Memory allocation ka kaam Python ke private heap me hota hai.




```python
x = 10  # Python heap me ek object banega jo `10` store karega.
y = "Hello"  # Ek string object banega jo "Hello" store karega.
```

### Private Heap

* Private Heap wo jagah hai jahan Python saare objects aur variables ki memory store karta hai.

* Is heap ka access directly programmer ke paas nahi hota.

* Python ke Memory Manager heap ko manage karta hai.

### Reference Counting

* Python me har object ke paas ek reference count hota hai, jo batata hai ki kitne variables ya objects usse refer kar rahe hain.

* Jab reference count 0 ho jata hai (matlab object ko koi refer nahi kar raha), to wo memory automatically free ho jati hai.


```python
x = 10  # Reference count of object `10` is 1.
y = x   # Reference count of `10` increases to 2.
del x   # Reference count of `10` decreases to 1.
del y   # Reference count of `10` becomes 0, memory is freed.
```

### Garbage Collection

* Python me ek Garbage Collector (GC) hota hai jo unused objects ki memory free karta hai.

* GC circular references ko bhi handle karta hai (jaha do objects ek dusre ko refer karte hain, par koi unhe refer nahi kar raha).


```python
class Node:
    def __init__(self):
        self.ref = None

# Create circular reference
a = Node()
b = Node()
a.ref = b
b.ref = a

# Even if you delete `a` and `b`, their references to each other cause a memory leak.
# Garbage collector handles this situation in Python.
del a
del b

```

# Explain method overriding and method overloading.


###  Method Overriding

Method overriding tab hota hai jab ek child class apne parent class ke method ko redefine karti hai, taki wahi method child class ke context me alag behavior dikhaye.

#### Key Points:

1. Same Name, Same Parameters:

* Method overriding me parent aur child class ke methods ka naam aur parameters same hote hain.

2. Inheritance:

* Ye inheritance ka concept use karta hai.

3. Dynamic Dispatch:

* Jab object ko call kiya jata hai, to Python runtime pe decide karta hai ki child class ka method use karna hai ya parent class ka.


```python
class Parent:
    def greet(self):
        return "Hello from Parent!"

class Child(Parent):
    def greet(self):  # Overriding parent method
        return "Hello from Child!"

# Create objects
parent_obj = Parent()
child_obj = Child()

print(parent_obj.greet())  # Output: Hello from Parent!
print(child_obj.greet())   # Output: Hello from Child!

```

### Method Overloading

Python me strict method overloading ka concept nahi hai jaise C++ ya Java me hota hai. Python me same method ko different number of arguments ke sath implement karna loosely method overloading kehlata hai.

Python me default arguments ya *args aur **kwargs ka use karke method overloading ko achieve karte hain.

##### Key Points:

1. Same Name, Different Parameters:

* Method overloading me ek hi method ka naam same hota hai, par parameters alag-alag hote hain (count ya type ke hisaab se).

2. No True Overloading in Python:

* Python me ek hi naam ka multiple methods define nahi kar sakte. Last defined method hi active rahega.

3. Achieved via Default/Variable Arguments:

* Default arguments aur variable arguments (*args, **kwargs) ka use karke overloading ko achieve karte hain.


```python
# Example of Method Overloading (Using Default Arguments):

class Calculator:
    def add(self, a, b=0, c=0):  # Default arguments
        return a + b + c

calc = Calculator()
print(calc.add(5))        # Output: 5
print(calc.add(5, 10))    # Output: 15
print(calc.add(5, 10, 15))  # Output: 30

```


```python
# Example of Method Overloading (Using *args):

class Calculator:
    def add(self, *args):  # Accepts any number of arguments
        return sum(args)

calc = Calculator()
print(calc.add(5))           # Output: 5
print(calc.add(5, 10))       # Output: 15
print(calc.add(5, 10, 15))   # Output: 30
```

| **Feature**        | **Method Overriding**                                   | **Method Overloading**                                     |
| ------------------ | ------------------------------------------------------- | ---------------------------------------------------------- |
| **Definition**     | Child class me parent class ke method ko redefine karna | Same method name ke sath different parameters define karna |
| **Inheritance**    | Inheritance required                                    | Inheritance not required                                   |
| **Parameters**     | Parameters same hote hain                               | Parameters different hote hain                             |
| **Behavior**       | Child class method ka behavior use hota hai             | Method arguments ke basis pe behavior change hota hai      |
| **Python Support** | Fully supported                                         | True method overloading nahi, par achieve kar sakte hain   |


#### Summary 

#### Method Overriding:

* Jab child class parent class ke method ko same naam aur parameters ke sath redefine karti hai.

* Inheritance ka use hota hai.

* Dynamic dispatch se decide hota hai ki parent ya child method ka call hoga


```python
class Parent:
    def show(self):
        print("Parent method")

class Child(Parent):
    def show(self):  # Overriding
        print("Child method")
```

### Method Overloading:

* Jab ek hi method ko different parameters ke sath define karte hain.

* Python me default arguments ya *args ka use karke achieve karte hain.

* Inheritance ki zarurat nahi hoti.


```python
class Example:
    def display(self, a, b=0):
        print(a + b)
```
