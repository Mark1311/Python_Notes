#                                                       PYTHON QUESTION'S

## Doc.String in Python

Python mein docstring ek special type ki string hoti hai jo kisi function, class, ya module ke baare mein information provide karti hai. Yeh us function ya class ka purpose, parameters, aur return value ko describe karti hai. or ye always class ya function ke just niche likhi jati ha.

Docstring hamesha triple quotes (''' ya """) ke andar likhi jaati hai.

### Docstring ka use kyun karte hain?

1. Code ko samajhna aasaan banaana: Jab koi aur developer aapka code padhe, toh wo easily samajh sakta hai ki function kya karta hai 
aur kaise use kiya jaa sakta hai.

2.Docstring ek zaroori tareeka hai jo aapke code ko clean aur understandable banata hai. Isse code ki readability improve hoti
hai aur dusre developers ko aapka code samajhne mein aasani hoti hai.


```python
def add(a, b):
    """
    Yeh function do numbers ka sum karta hai.
    Parameters:
    a (int): Pehla number
    b (int): Dusra number
    Returns:
    int: Do numbers ka sum
    """
    return a + b

```

# Enumerate() Function

Enumerator function ek aisi function hoti hai jo kisi collection ya sequence (jaise list, tuple, string, ya kisi iterable object) 
ke elements ke index aur values ko return karti hai. Ye function generally enumerate() ke naam se jaana jaata hai.

enumerate() function ko kisi iterable object (like a list or string) ke saath use kiya jaata hai, aur yeh us iterable ke har 
element ke index aur value dono ko ek tuple ke form mein return karta hai.

Iska fayda yeh hai ki aapko index aur element ko separately handle karne ki zaroorat nahi padti.


```python
fruits = ['apple', 'banana', 'cherry']

# enumerate ko use karke index aur value dono ko print karte hain
for index, fruit in enumerate(fruits):
    print(index, fruit)

#Output here
# 0 apple
# 1 banana
# 2 cherry
```

### Use case:
Agar aap kisi list ke elements par kuch operations perform kar rahe ho aur uske index ko bhi zaroorat ho, to enumerate() kaafi helpful hai.

Jaise agar aapko ek list mein specific index par kuch update karna ho ya index ke basis pe kuch conditions check karna ho, to enumerate() 
use kar sakte hain.

Readability ko improve karta hai:

# Difference between Shallow and Deep copy

### Shallow Copy

Shallow copy nested list ko copy karta hai, lekin deeply copy nahi karta. Matlab, agar aap ek nested list ka shallow copy banate hain,
toh outer list ki copy ban jaati hai, lekin inner lists ya sublists ke references hi copy hote hain, unki actual copies nahi ban paati.

Iska matlab yeh hai ki agar aap shallow copy ko modify karte hain (especially inner lists ko), toh original list bhi uss change 
ko reflect karegi, kyunki inner lists ab bhi same memory location ka reference rakhte hain.


```python
# Original nested list
original_list = [[1, 2, 3], [4, 5, 6],8]

# Shallow copy of the original list
shallow_copy = copy.copy(original_list)

# Modifying the inner list of the shallow copy
shallow_copy[0][0] = 100

shallow_copy[2] = 1000

# Output
print("Original List:", original_list)  # Original list will also show the change
print("Shallow Copy:", shallow_copy)    # Shallow copy will show the change as well

```

### Deep Copy

Deep copy nested list ko full copy karta hai. Iska matlab hai ki deep copy not just the outer list, but inner lists (or sublists) 
ko bhi independent copies banaata hai. Jab aap deep copy ka use karte hain, har ek nested element ka apna separate copy banta hai, 
jisse original list aur copied list ek doosre se bilkul independent ho jaati hain.
# Original nested list
original_list = [[1, 2, 3], [4, 5, 6],55]

# Deep copy of the original list
deep_copy = copy.deepcopy(original_list)

# Modifying the inner list of the deep copy
deep_copy[0][0] = 100

deep_copy[2] = 122

# Output
print("Original List:", original_list)  # Original list will remain unchanged
print("Deep Copy:", deep_copy)  

# Decerorater

`How Decorators Work:`
A decorator is a function that takes another function as an argument and returns a new function that enhances or alters the 
behavior of the original function.

Python mein decorator ek special function hota hai jo kisi doosre function ko modify ya enhance karta hai bina uske original code ko badle. 
Yeh ek aise function ka kaam karta hai jo dusre function ko "wrap" karke uske behavior ko change karta hai.

Aap samajh sakte hain ki ek decorator ek wrapper hai jo aapke function ke upar laga hota hai aur uske kaam ko badalta hai. 
Iska use commonly function ya method ko modify karne ke liye kiya jata hai, jaise ki logging, access control, timing, etc.

Maan lo ki ek function hai greet jo ek simple greeting print karta hai. Ab agar aap chahein ki is function se pehle ya baad mein 
kuch aur kaam ho, to aap ek decorator ka use kar sakte hain.


```python
def my_decorator(func):
    def wrapper():
        print("Before the function is called")
        func()
        print("After the function is called")
    return wrapper

@my_decorator  # This is a decorator syntax
def greet():
    print("Hello, World!")

greet()
```

Yahan pe, @my_decorator syntax use kar ke hum greet function ko wrap kar rahe hain. Jab aap greet() call karenge, to pehle 
"Before the function is called" print hoga, phir greet ka actual kaam hoga (i.e., "Hello, World!"), aur finally 
"After the function is called" print hoga.

# What is PIP

Pip Installs Packages or Preferred Installer Program

Pip ek Python ka tool hai jo aapko external libraries ya packages ko easily install, update, ya remove karne mein madad karta hai. 
Matlab, jab aapko Python mein koi extra features chahiye hote hain jo Python ke standard library mein nahi hote, 
tab aap pip ka use karte hain.

Ye Python Package Index (PyPI) se connect hota hai jahan par sabhi Python packages store hote hain.

Aur haan, agar aapke paas Python 3.4 ya usse upar ka version hai, toh pip pehle se hi installed hota hai!

# MODULE & PACKAGE & Library

### Python Module:-

Module ek single Python file hota hai jo Python code ko organize karta hai.
Ye file .py extension ke saath hoti hai. Matlab, jab aap kisi file ko create karte ho, jaise my_module.py, toh wo ek module hai.
Is file mein aap variables, functions, classes, etc. define kar sakte ho, aur baad mein is file ko import karke use kar sakte ho.

### Python Package
Package ek folder hota hai jo kai modules ko organize karta hai. Matlab, package mein multiple Python files (modules) ho sakti hain.
Package ko recognize karne ke liye us folder mein ek special file __init__.py hoti hai. Iska kaam ye hota hai ki Python ko bataye ki ye 
ek package hai.
Ek package aapko multiple related modules ko ek jagah pe rakhne ka tareeka deta hai.


Example: Maan lo aapke paas ek folder hai math_package jisme do files hain: addition.py aur subtraction.py. Aur is folder mein 
ek __init__.py file bhi hai, jo Python ko batata hai ki ye ek package hai.

Summary:
Module ek single .py file hoti hai, jo functions, classes, aur variables ko organize karti hai.
Package ek folder hota hai, jo multiple modules ko group karta hai, aur us folder mein ek __init__.py file hoti hai jo package ko 
define karti hai.


### Library

Library ek collection hota hai modules ka. Matlab ek library mein kai sare modules hote hain jo specific tasks ko perform karte hain.

Libraries zyada general hoti hain aur kaafi functionalities provide karti hain, jaise ki data analysis, web development, 
ya machine learning.

Example: NumPy ek library hai, jo kai sare modules aur functions provide karti hai jo arrays aur mathematical operations ke liye use hote hain.

`Module:` Ek single .py file jisme code hota hai (jaise math_operations.py).

`Package:` Ek folder jisme multiple modules hote hain (jaise math_package folder).

`Library:` Multiple modules ya packages ka collection hota hai, jo ek common functionality provide karte hain (jaise NumPy ya Pandas).

# Compare b/w Module, Library and Package?

Module (मॉड्यूल):-

A module is just a single file containing Python code (with a .py extension). It can contain functions, classes, or variables, and it can 
also include runnable code.
`Example:` If you have a file named math_functions.py, that file is a module.

Library (लाइब्रेरी):-

A library is a collection of modules that are related and packaged together to perform a specific set of tasks. It is usually a collection of many modules.

`Example:-` NumPy is a library for numerical computations and contains many modules to handle arrays, mathematical operations, etc.
Libraries are often large and can include multiple modules inside them.

`Example:` When you install NumPy using pip install numpy, you are installing a library, which includes many modules for numerical operations.

Package (पैकेज):-

A package is a collection of Python modules that are grouped together in a directory and are organized in a hierarchical structure (can contain sub-packages).

A package usually has a special file named __init__.py inside the folder to tell Python that the directory should be treated as a package.

`Example:` Pandas is a package for data manipulation and analysis. It contains multiple modules inside the package.


# Inheritance in Python

Inheritance ka matlab hai ek class apne parent class se properties aur methods inherit kar sakti hai. 
Matlab ek class dusri class se functionality ko "adopt" kar sakti hai.

Agar ek Animal class hai jisme eat method hai, toh koi bhi specific animal, jaise Dog ya Cat, us Animal class se ye 
method inherit kar sakte hain.


```python
### Single Inheritance (Ekla Class Inheritance)

Isme ek class sirf ek parent class se properties aur methods inherit karti hai.

# Parent class
class Animal:
    def speak_animal(self):
        print("Animal makes a sound")

# Child class inheriting from Animal
class Dog(Animal):
    def speak(self):
        print("Dog barks")

# Create object of Dog
dog = Dog()
dog.speak_animal()  # Output: Dog barks

```


```python
### Multiple Inheritance (Multiple Classes se Inheritance): 

Isme ek class ek se zyada parent classes se properties aur methods inherit karti hai.

# Parent class 1
class Animal:
    def speak_animal(self):
        print("Animal makes a sound")

# Parent class 2
class Pet:
    def info(self):
        print("This is a pet")

# Child class inheriting from both Animal and Pet
class Dog(Animal, Pet):
    def speak(self):
        print("Dog barks")

# Create object of Dog
dog = Dog()
dog.speak_animal()  # Output: Dog barks
dog.info()   # Output: This is a pet
dog.speak()  # Dog barks

```


```python
### Multilevel Inheritance (Ek ke baad ek Inheritance): 

Isme ek class doosri class se inherit karti hai, aur fir wo class kisi aur class se inherit karti hai.

# Grandparent class
class Animal:
    def speak_animal(self):
        print("Animal makes a sound")

# Parent class
class Dog(Animal):
    def speak_dog(self):
        print("Dog barks")

# Child class
class Puppy(Dog):
    def speak(self):
        print("Puppy whines")

# Create object of Puppy
puppy = Puppy()
puppy.speak_animal()  # Output: Puppy whines
puppy.speak()
puppy.speak_dog()

```


```python
### Hierarchical Inheritance (Ek hi Parent se multiple Children): 

Isme ek parent class multiple child classes ko properties aur methods deti hai.

# Parent class
class Animal:
    def speak_animal(self):
        print("Animal makes a sound")

# Child class 1
class Dog(Animal):
    def speak_dog(self):
        print("Dog barks")

# Child class 2
class Cat(Animal):
    def speak(self):
        print("Cat meows")

# Create objects of Dog and Cat
dog = Dog()
cat = Cat()

dog.speak_animal()  # Output: Animal makes a sound
cat.speak_animal()  # Output: Animal makes a sound

```


```python
### Hybrid Inheritance (Multiple aur Multilevel ka combination): 

Isme multiple aur multilevel inheritance ka combination hota hai.

# Parent class 1
class Animal:
    def speak(self):
        print("Animal makes a sound")

# Parent class 2
class Pet:
    def info(self):
        print("This is a pet")

# Child class 1 inheriting from Animal
class Dog(Animal):
    def speak(self):
        print("Dog barks")

# Child class 2 inheriting from both Animal and Pet
class Cat(Animal, Pet):
    def speak(self):
        print("Cat meows")

# Create objects of Dog and Cat
dog = Dog()
cat = Cat()

dog.speak()  # Output: Dog barks
cat.speak()  # Output: Cat meows
cat.info()   # Output: This is a pet
```

#### Summery

`Single Inheritance:` One parent class, one child class.

`Multiple Inheritance:` One child class inherits from multiple parent classes.

`Multilevel Inheritance:` A child class inherits from another child class, forming a hierarchy.

`Hierarchical Inheritance:` Multiple child classes inherit from a single parent class.

`Hybrid Inheritance:` A combination of more than one type of inheritance.

# OOP's Concept

OOP (Object-Oriented Programming) ek programming concept hai jo real-world objects ko model karne ke liye use hota hai. 
Iska main idea ye hai ki hum apni programming ko objects aur classes ke around organize karte hain. 
OOP ka goal hota hai ki hum software ko aise structure karein jo real world ke cheezon se closely relate kare,jisme behavior 
aur data dono ek saath rakhe jaate hain.

`Encapsulation:` Data ko hide karna aur specific methods se access karna.

`Inheritance:` Ek class dusri class se properties aur methods inherit kar sakti hai.

`Polymorphism:` Same method ka alag behavior alag classes me ho sakta hai.

`Abstraction:` Sirf important details ko dikhana, baaki ko hide karna.

# Implicit and Explicity type coversion

#### Implicit Type Conversion (Automatic Type Conversion):

Implicit type conversion tab hota hai jab programming language khud se data types ko change kar leti hai, bina humare intervention ke. 
Matlab, agar hum ek type ka data doosre type mein assign karte hain, aur language ko lagta hai ki conversion possible hai, 
to woh khud hi conversion kar deti hai. Yeh automatic hota hai.

Example in Hinglish:
Agar aap ek integer ko float mein assign karte ho, to language apne aap woh integer ko float mein convert kar degi.



```python
x = 10   # int type
y = 5.5  # float type
result = x + y  # Python will automatically convert x to float and perform the addition.
print(result)  # Output: 15.5
```

#### Explicit Type Conversion (Manual Type Conversion):
Explicit type conversion tab hota hai jab hum khud se data type ko change karte hain, yaani manually. 
Hum programming mein functions ka use karte hain jisse hum data type ko apne hisaab se convert kar sakein.

Example in Hinglish:
Agar aap float ko integer mein convert karna chahte ho, to aap explicitly int() function use karte ho.



```python
x = 10.7  # float type
result = int(x)  # Manually converting float to int
print(result)  # Output: 10
```

# Super() Keyword

Python mein super() ek built-in function hai jo aapko parent class ke methods ko child class se access karne mein madad karta hai. 
Ye inheritance mein kaafi useful hota hai, jahan aap child class mein parent class ke methods ko override karte hain, 
lekin kabhi-kabhi parent class ke behavior ko bhi reuse karna chahte hain.

`super() ka use kahan hota hai?`

Parent class ke methods ko call karne ke liye: Jab aap child class mein method override karte hain, tab aap super() ka use karke parent 
class ke method ko call kar sakte hain.

Agar child class aur parent class dono me same method ka naam ho, to super() se hum parent class wala version call kar sakte hain.


`super() almost har type ke inheritance me use ho sakta hai, lekin mainly yeh method overriding wale cases me powerful hota hai.`


```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def __init__(self, name, breed):
        # super() ka use kar ke Animal class ka __init__ method call kar rahe hain
        super().__init__(name)
        self.breed = breed
    
    def speak(self):
        # super() ka use kar ke Animal class ka speak method call kar rahe hain
        super().speak()
        print(f"{self.name} barks")

# Dog class ka object banate hain
dog = Dog("Tommy", "Golden Retriever")
dog.speak()
```

super().__init__(name): Ye Animal class ka __init__ method call kar raha hai, jisme name ko initialize kiya jata hai. 
Agar hum super() ka use na karte, toh hume manually Animal class ka constructor call karna padta.

super().speak(): Ye Animal class ka speak() method call kar raha hai, jisme basic sound print hoti hai. 
Uske baad Dog class mein humne apni specific behavior add kiya hai ("barks").

## 🔥 Without super() — Problem:-

Agar hum parent class ka method manually call karein, to code rigid ho jata hai aur maintain karna mushkil hota hai.


```python
class Parent:
    def show(self):
        print("Parent show")

class Child(Parent):
    def show(self):
        print("Child show")
        Parent.show(self)  # parent ko manually call karna pad raha hai

c = Child()
c.show()

#Output:- Child show
#         Parent show
```

### ⚠️ Jaha use nahi hota

`Agar inheritance use hi nahi ho raha — to super() ki zaroorat nahi.`

`Agar parent method override nahi kiya — to super() ki need nahi hoti`

# *arg and **kwarg diff..?

### *args (Positional Arguments):-

*args ka use variable number of positional arguments ko accept karne ke liye hota hai.
args ek tuple ki tarah behave karta hai, jisme aap multiple values pass kar sakte hain.
Agar aapko pata na ho ke function ko kitne arguments diye jayenge, to aap *args ka use karte hain.



```python
def sum_numbers(*args):
    total = sum(args)
    return total

print(sum_numbers(1, 2, 3))  # Output: 6
print(sum_numbers(10, 20, 30, 40))  # Output: 100
```

### **kwargs (Keyword Arguments):-

**kwargs ka use variable number of keyword arguments ko accept karne ke liye hota hai.
kwargs ek dictionary ki tarah behave karta hai, jisme aap key-value pairs pass kar sakte hain.
Agar aapko pata na ho ke function ko kis naam ke arguments diye jayenge, to **kwargs ka use hota hai.



```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Ali", age=25, country="Pakistan")

#### Output:

#  name: Ali
#  age: 25
#  country: Pakistan
```

    name: Ali
    age: 25
    country: Pakistan
    

### *args aur **kwargs Ek Sath:


```python
def complete_function(positional_arg, *args, **kwargs):
    print(f"Positional Argument: {positional_arg}")
    print("Args:", args)
    print("Kwargs:", kwargs)

complete_function(10, 20, 30, name="Bittu", age=25)
# Output:
# Positional Argument: 10
# Args: (20, 30)
# Kwargs: {'name': 'Bittu', 'age': 25}

```

### Difference:- 

`*args` positional arguments ke liye hota hai, jisme values sequence ke hisaab se pass hoti hain.
    
`**kwargs` keyword arguments ke liye hota hai, jisme keys aur values key-value pair ke form mein pass hoti hain.

# Self Keyword:- 

Python mein self ek special keyword hai jo instance methods ke andar use hota hai. Ye class ke instance ko represent 
karta hai, jise hum method ke first parameter ke roop mein pass karte hain.

Jab hum ek object bana kar kisi class ka method call karte hain, to self keyword ke zariye wo method us object ka 
reference le leta hai. Ye method ko apne object ke attributes aur methods ko access karne ka option deta hai.

### self kya hota hai..?

Jab aap koi class banate ho aur usme methods likhte ho, toh har method ko apne object ka reference chahiye hota hai.
Python mein, self ko use karke method ko uss specific object ka reference diya jata hai.
Matlab jab aap method call karte ho, to self us object ka pointer ho jata hai jisse method call ho raha hai.

### Method ko kis object ka reference chahiye hota hai?
Jab aap class ke kisi instance ko create karte hain, jaise dog1 = Dog("Buddy", 3), tab aapka object dog1 ban gaya.
Ab jab aap dog1.bark() call karte ho, Python internally dog1 ko self ke roop mein method ke andar pass karta hai.



```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand  # self.brand object ka attribute hai
        self.model = model  # self.model object ka attribute hai

    def display_info(self):
        print(f"Car Brand: {self.brand}")
        print(f"Car Model: {self.model}")

# Object create karte hain
car1 = Car("Toyota", "Corolla")
car2 = Car("Honda", "Civic")

# Methods ko call karte hain
car1.display_info()
car2.display_info()

```

    Car Brand: Toyota
    Car Model: Corolla
    Car Brand: Honda
    Car Model: Civic
    

### Why self is Important:
Agar self na hota, to aapke methods ko yeh nahi pata hota ki kis object ka data access karna hai.
self ka use karke aap apne objects ke attributes ko safely manage kar sakte hain.

### self ka role:
Object-specific: self aapke method ko object-specific banaata hai.
Accessing object attributes: self ka use karke aap kisi bhi object ka data access kar sakte ho.
Multiple objects: Aap ek class ke multiple objects bana sakte ho aur self ke through har object ka alag data manage kar sakte ho.

### Conclusion:
self ek special reference hai jo method ke through current object ko access karne ke liye use hota hai.
Har instance method ko self ka parameter chahiye hota hai taaki wo apne object ka state track kar sake.
Python mein, self ko manually pass karne ki zarurat nahi hoti; Python apne aap yeh kaam kar leta hai jab aap object 
ka method call karte hain.


# map(), filter(), and Reduce() function

map(), filter(), aur reduce() Python mein built-in higher-order functions hote hain jo iterable objects (jaise lists, tuples) par operate karte hain. Inka use hum data processing mein karte hain, jaise transformations, filtering, aur accumulation. In functions ka major difference unki functionality mein hota hai:

`map():
`
function ek given function ko iterable ke har item par apply karta hai aur result ko ek new iterable (map object) 
ke roop mein return karta hai.

Nahi, map() function Python mein original list ko change nahi karta hai. 
map() function ek new iterable return karta hai, jo ke har element par ek specified function apply kar ke banata hai. Original list ko koi bhi change nahi hoti

Syntax: map(function, iterable)


```python
numbers = [1, 2, 3, 4, 5]
squared = map(lambda x: x**2, numbers)
print(list(squared))  # Output: [1, 4, 9, 16, 25]
```


```python
# List of numbers
numbers = [1, 2, 3, 4, 5]

# Function to calculate square
def square(x):
    return x * x

# Applying map
squared_numbers = map(square, numbers)
print(list(squared_numbers))  # Output: [1, 4, 9, 16, 25]
```

`filter():`
function ek given function ko iterable ke har item par apply karta hai aur sirf un items ko return karta hai jahan 
function True return kare. Basically, ye filter karne ka kaam karta hai.

filter() function bhi Python mein original list ko change nahi karta hai. filter() ek new iterable return karta hai jisme sirf woh elements hote hain jo given condition (function) ko satisfy karte hain.bss new list return krta ha.

Syntax: filter(function, iterable)



```python
numbers = [1, 2, 3, 4, 5]
even_numbers = filter(lambda x: x % 2 == 0, numbers)
print(list(even_numbers))  # Output: [2, 4]
```


```python
# List of numbers
numbers = [10, 15, 20, 25, 30]

# Function to check if a number is divisible by 5
def is_divisible_by_five(x):
    return x % 5 == 0

# Applying filter
divisible_by_five = filter(is_divisible_by_five, numbers)
print(list(divisible_by_five))  # Output: [10, 15, 20, 25, 30]

```

`reduce():`

reduce() function ko functools module se import karna padta hai. Ye ek accumulated result generate karta hai by applying a 
given function cumulatively to the items in an iterable. Iska output ek single value hota hai.

Syntax: reduce(function, iterable, [initial])


```python
from functools import reduce
numbers = [1, 2, 3, 4, 5]
sum_result = reduce(lambda x, y: x + y, numbers)
print(sum_result)  # Output: 15
```

    15
    


```python
from functools import reduce

# List of numbers
numbers = [1, 2, 3, 4, 5]

# Function to multiply two numbers
def multiply(x, y):
    return x * y

# Applying reduce
product = reduce(multiply, numbers)
print(product)  # Output: 120
```

`Purpose:`
* map(): Transform each item in an iterable.
* filter(): Filter items based on a condition.
* reduce(): Cumulatively reduce iterable to a single value.

`Output:`
* map(): Returns an iterable with transformed items.
* filter(): Returns an iterable with items that satisfy the condition.
* reduce(): Returns a single accumulated value.
    
`Function Type:`
* map() aur filter() functions iterable ko return karte hain.
* jabki reduce() ek single value return karta hai.

`Input aur Output:`

* map(): Aap jo function dete ho, woh har element par apply hota hai aur result ek nayi iterable mein hota hai.
* filter(): Aap jo function dete ho, woh elements ko condition ke basis par filter karta hai aur True wale elements ko return karta hai.
* reduce(): Aap jo function dete ho, woh elements ko accumulate karke ek single value return karta hai.

`Use Cases:`

* map() ka use tab karte hain jab humein kisi list (ya iterable) ke har element par koi operation perform karna ho (jaise transformation).
* filter() ka use tab karte hain jab humein kuch specific elements ko filter karna ho (jaise filtering even numbers).
* reduce() ka use tab karte hain jab humein kisi operation (sum, multiplication, etc.) ke result ko accumulate karna ho, aur 
ek final single value chahiye ho.

`Conclusion:`
* map(): Aap jab chahte hain ki har element par ek operation apply ho.
* filter(): Aap jab specific condition ke basis par elements ko filter karte ho.
* reduce(): Aap jab cumulative calculation karna chahte ho aur ek final value chahiye ho.

# if__name__=="__main__"


if __name__ == "__main__": ek conditional statement hai jo Python mein commonly use hota hai, especially jab aap 
code ko modules mein divide karte hain.

Iska kaam yeh hai ke jab aap kisi Python script ko direct execute karte hain, toh yeh condition True hoti hai. 
Agar aap usi script ko import karte hain kisi aur Python script mein, toh yeh condition False ho jati hai.



```python
# file1.py

def greet():
    print("Hello, World!")

if __name__ == "__main__":
    greet()

```

    Hello, World!
    

Agar aap file1.py ko directly run karte ho, toh greet() function call hoga, aur "Hello, World!" print hoga.

Agar aap file1.py ko kisi aur script mein import karte ho, toh greet() function call nahi hoga automatically.

Yeh condition ensure karti hai ke koi code sirf tab run ho jab script ko direct execute kiya ja raha ho, na ke jab usse import kiya ja raha ho. Isse code ka reuse aur modularity improve hoti hai.

`__name__ kya hai?`

__name__ ek special variable hai jo Python har module ke andar automatically set karta hai. Jab bhi aap koi Python
file likhte ho, uss file ko ek module ke roop mein treat kiya jata hai.

Agar aap script ko directly run kar rahe ho (e.g., python script.py), toh __name__ ka value "__main__" hota hai.
Agar aap usi script ko kisi doosri script mein import karte ho (e.g., import script), toh __name__ ka value script ke 
filename ke barabar hota hai.

`if __name__ == "__main__": ka use?`

Iska main purpose yeh hota hai ke aap apne code ko achhe se modularize kar sakein. Matlab, aap ek hi script ko as a module 
bhi use kar sakein aur agar aap chahein toh usse directly bhi run kar sakein bina kisi problem ke.


```python
# script.py
def hello():
    print("Hello from script!")

if __name__ == "__main__":
    print("This script is being run directly")
    hello()
else:
    print("This script has been imported")


1. Jab aap script ko directly run karenge:-

Output:-
This script is being run directly
Hello from script!

2. Jab aap script ko import karenge kisi doosri script mein:-

Output:
This script has been imported.
```

### Real-World Scenario
Imagine karen ke aapne ek file banayi hai jisme kuch utility functions hain, aur aap us file ko dusri scripts mein 
import kar ke use karte hain. Aap chahte hain ki jab aap us file ko directly run karein, toh kuch testing ya specific actions ho. 
Lekin jab aap us file ko import karenge, toh wo actions na ho.

Aise situation mein if __name__ == "__main__": aapko allow karta hai ke aap specific code ko sirf tab run karen jab script direct 
run ho raha ho, na ke jab wo import ho raha ho.

# Class and Instance variable?

Class variables aur instance variables, Python mein object-oriented programming ke concepts hain. Inko samajhna thoda important hai jab hum classes aur objects ki baat karte hain. Dono ka apna role hota hai.

`Class Variables:- `


Class variables wo variables hote hain jo ek class ke sare objects ke liye common hote hain.
Ye variable class level pe define kiye jaate hain, na ki kisi specific instance (object) ke liye.
Inki value agar change hoti hai, toh wo sabhi objects pe affect karti hai jo us class se belong karte hain.

Class Level Pe Define Hote Hain: Ye variables class ke andar hi directly define kiye jaate hain, lekin self ka use nahi hota.
Shared Between All Objects: Agar ek class ka class variable hai, toh usko sabhi instances (objects) ek hi value share karte hain.



```python
class Car:
    wheels = 4  # Class variable, ye sab cars ke liye common hai

car1 = Car()
car2 = Car()

print(car1.wheels)  # 4
print(car2.wheels)  # 4

# Agar class variable ko change karenge
Car.wheels = 6
print(car1.wheels)  # 6
print(car2.wheels)  # 6
```

`Instance Variables:- `

Instance variables wo variables hote hain jo ek specific object ke liye define kiye jaate hain.
Ye har object ka apna alag state rakhta hai. Matlab, ek object ka instance variable dusre object ke instance variable se alag hota hai.
Inki value change karne se sirf wahi specific object pe affect hota hai.

Object Level Pe Define Hote Hain:- Ye variables self ke through object ke saath associated hote hain. Matlab har object ke paas apna alag 
instance variable hota hai.
Unique to Each Object:-  Agar ek object ka instance variable badalta hai, toh wo dusre object pe affect nahi karega.


```python
class Car:
    def __init__(self, color):
        self.color = color  # Instance variable, har car ka color alag ho sakta hai

car1 = Car("Red")
car2 = Car("Blue")

print(car1.color)  # Red
print(car2.color)  # Blue

# Agar instance variable ko change karenge
car1.color = "Green"
print(car1.color)  # Green
print(car2.color)  # Blue
```

### Important Differences

`Class Variables:`

* Common hote hain.
* Sab objects mein shared hote hain.
* Agar class variable ki value change hoti hai, toh wo sabhi objects ko effect karti hai.
    
`Instance Variables:`

* Object-specific hote hain.
* Har object ka apna state hota hai.
* Agar ek object ka instance variable change hota hai, toh wo sirf ussi object ko effect karta hai, baaki objects ko nahi.

1. Class Variables: Class level pe defined hote hain, sab objects ke liye common hote hain.
2. Instance Variables: Object level pe defined hote hain, har object ka apna unique value hota hai.
3. Class variables ko class level pe define kiya jaata hai, aur wo sabhi objects mein shared hote hain.
4. Instance variables ko object level pe define kiya jaata hai, aur har object ka apna alag instance variable hota hai.

# Assess Modifiere (Public, Provate and Protective A.M.)

Python me access modifiers ka use class ke andar variables aur methods ki visibility control karne ke liye kiya jata hai. 
Ye modifiers decide karte hain ki kisi variable ya method ko kis class ya object ke outside access kiya ja sakta hai ya nahi.

Python mein 3 types ke access modifiers hote hain:

* Public (by default)
* Protected
* Private

`1. Public Access Modifier:`

Public members wo hote hain jo class ke bahar se access kiye ja sakte hain.

Class ke andar, bahar, object ke through kahin se bhi access ho sakte hain.

Python me, agar aap kisi variable ya method ke aage koi access modifier nahi lagate, to wo public hota hai by default.

Aap directly isko access kar sakte hain.


```python

class MyClass:
    def __init__(self):
        self.name = "Python"

    def display(self):
        print("Hello, " + self.name)

# Creating object of class
obj = MyClass()

# Accessing public variable
print(obj.name)  # Output: Python

# Accessing public method
obj.display()  # Output: Hello, Python
```

    Python
    Hello, Python
    

`2. Protected Access Modifier:`

Protected members wo hote hain jo class aur subclass ke andar access kiye ja sakte hain, lekin class ke bahar directly 
access nahi kiye ja sakte(but technically possible).

Python mein, protected variables aur methods ko underscore (_) se denote kiya jata hai.


```python
class MyClass:
    def __init__(self):
        self._name = "Python"

    def _display(self):
        print("Hello, " + self._name)

# Creating object of class
obj = MyClass()

# Accessing protected variable (not recommended outside class)
print(obj._name)  # Output: Python

# Accessing protected method (not recommended outside class)
obj._display()  # Output: Hello, Python
```

    Python
    Hello, Python
    

`3. Private Access Modifier:`

Private members wo hote hain jo sirf class ke andar hi access kiye ja sakte hain, aur bahar se unhe access nahi kiya ja sakta.

Python me, private members ko double underscore (__) se denote kiya jata hai.



```python
class MyClass:
    def __init__(self):
        self.__name = "Python"

    def __display(self):
        print("Hello, " + self.__name)

# Creating object of class
obj = MyClass()

# Trying to access private variable (will cause error)
# print(obj.__name)  # This will give an AttributeError

# Trying to access private method (will cause error)
# obj.__display()  # This will give an AttributeError

# obj._MyClass__display() # Outout -> Hello, Python
```

    Hello, Python
    

`Conclusion:`

Public: Sabhi jagah se access ho sakte hain.

Protected: Sirf class aur subclass se access kiye ja sakte hain.

Private: Sirf class ke andar access kiye ja sakte hain (direct access possible nahi hai).

| Modifier  | Syntax  | Access Area               | Allowed in Inheritance                   |
| --------- | ------- | ------------------------- | ---------------------------------------- |
| Public    | `var`   | Everywhere                | ✔ Yes                                    |
| Protected | `_var`  | Within class + subclasses | ✔ Yes                                    |
| Private   | `__var` | Only within same class    | ❌ No (direct), name-mangling se possible |


# Clouser

Closures ek programming concept hota hai jo mostly functional programming languages mein use hota hai. Python, JavaScript, 
aur C++ jaise languages mein closures ka concept implement kiya jaata hai.

Closure ka matlab hai, ek function jo apne enclosing (outer) function ke variables ko access kar sakta hai, even after wo outer 
function execute ho chuki hoti hai.

`Simple Example:`
Agar ek function outer ke andar ek function inner defined hai aur inner function outer ke variables ko use karta hai, 
toh inner function closure ban jaata hai.


```python
def outer(x):
    def inner(y):
        return x + y
    return inner

closure_function = outer(10)
print(closure_function(5))  # Output: 15
```


Yahan par closure_function ek closure hai jo outer function ke x variable ko access kar raha hai, even though outer 
function ka execution complete ho gaya tha.

Closure ka major benefit yeh hota hai ki wo state ko preserve kar sakta hai aur functions ko encapsulate karke reusability 
ko enhance karta hai.


```python
def outer(x):
    def inner(y):
        return x + y
    return inner

closure_function = outer(10)
print(closure_function(5))  # Output: 15
```

1. outer function ko jab call kiya jaata hai, toh x variable ko initialize kiya jaata hai.

2. inner function ko outer function ke andar define kiya gaya hai, aur yeh x ko access kar sakta hai. Isliye inner ko closure kaha jaata hai.

3. Jab outer(10) call kiya jaata hai, x ki value 10 ho jaati hai. outer function ke execution ke baad, inner function ko return kar diya jaata hai.

4. Ab closure_function jo inner function ka reference hai, usmein ab bhi x = 10 ko yaad rakha gaya hai.

5. Jab closure_function(5) ko call kiya jaata hai, toh inner function mein y = 5 hota hai, aur x ki value jo outer ke scope mein thi, woh bhi accessible hoti hai (i.e., x = 10).

Toh, closure x ki value ko yaad rakhkar kaam karta hai aur x ke value ke saath kaam karta hai jab tak closure call hota hai.

# Class, Object, Instance and Method kya hote ha?

`1. Class:`
Class ek blueprint ya template hoti hai jisme kisi object ki properties (variables) aur behaviors (methods) define kiye jate hain. 
Matlab, ek class kisi cheez ka design hai.



```python
class Car:
    # Properties (Variables)
    brand = "Toyota"
    model = "Corolla"
    
    # Behaviors (Methods)
    def start(self):
        print("Car is starting")
        
    def stop(self):
        print("Car is stopping")
```

`2. Object:`
Object class ka ek specific instance hota hai. Jab hum class ko use karte hain, tab hum ek object banate hain. 
Ek class ke multiple objects banaye ja sakte hain, aur har object apne aap mein unique hota hai.


```python
# Creating an object of the Car class
my_car = Car()
```

`3. Instance:`
Instance bhi object hi hota hai, magar jab hum ek object ko class ka part bana lete hain, to hum usko "instance" kehte hain. 
Basically, instance ek object ka real-world representation hai jo class ka ek copy hota hai.


```python
# Here, 'my_car' is an instance of the Car class
print(my_car.brand)  # Output: Toyota
```

`4. Method:`
Method ek function hoti hai jo class ke andar define hoti hai. Yeh class ke objects ke behavior ko define karti hai,
matlab kya action perform karna hai. Method ko call karke hum object ke behavior ko change kar sakte hain.



```python
# Calling methods of the 'my_car' object
my_car.start()  # Output: Car is starting
my_car.stop()   # Output: Car is stopping
```

`Summary:`
* Class: Blueprint ya template hoti hai jo define karti hai ki object ki properties aur behavior kya honge.
* Object: Class ka ek specific instance, jo real-world entity ka representation hota hai.
* Instance: Object ka real-world example, jo class ka ek copy hota hai.
* Method: Class ke andar ka function jo object ka behavior define karta hai.

# Generator 

Python mein generator ek special type ka iterator hota hai jo values ko lazy way mein generate karta hai, yani ek time par sirf 
ek value generate hoti hai aur memory mein store nahi hoti. Iska matlab hai ki agar aapko bohot saari values ka sequence chahiye, 
to generator unko ek-ek karke produce karega jab zarurat ho, instead of ek baar mein saari values ko memory mein rakhne ke.


Generator kaise kaam karta hai?
Generator ko define karte waqt hum yield keyword ka use karte hain. yield ek value return karta hai aur function ko 
suspend karta hai, phir jab next value ki zarurat hoti hai to function wahan se dobara continue hota hai.


```python
def my_generator():
    yield 1
    yield 2
    yield 3

gen = my_generator()

# Values ko print karte hain ek-ek karke
print(next(gen))  # Output: 1
print(next(gen))  # Output: 2
print(next(gen))  # Output: 3

```

Is example mein, my_generator function ek generator object return karta hai. Jab hum next() call karte hain, to har bar ek new value 
milti hai, aur function ko suspend kar diya jata hai jab tak agla next() call nahi hota.

Aapko generators ka use kabhi karna padta hai jab aapko large datasets ya long-running sequences ke sath kaam karna ho, 
aur aapko performance aur memory ko optimize karna ho.

Generator ke benefits:-

Memory efficient: Generators large sequences ko handle karte waqt kam memory consume karte hain.
Lazy evaluation: Jab tak kisi value ki zarurat na ho, tab tak woh generate nahi hoti.
Performance improvement: Agar aapko sirf kuch values ki zarurat ho, to pura sequence generate karne ki bajaye aap sirf required 
values ko generate kar sakte hain.

# Polymorphism 

Polymorphism ek concept hai jo object-oriented programming (OOP) mein use hota hai. Iska matlab hai "many forms" yaani ki ek object ya method ko alag-alag tareekon se use karna. Iska basic idea yeh hai ke ek hi name ya method ko alag-alag types ya forms mein use kiya ja sakta hai, depending on the context.

# Types of Polymorphism

### Compile-time Polymorphism (Static Polymorphism)

1. Compile-time Polymorphism (Static Polymorphism) ek aisi polymorphism hai jo program ke compile hone ke waqt resolve hoti hai. Isme method overloading aur operator overloading ka concept aata hai.

Iska matlab hai ke polymorphism ko compile ke waqt resolve kiya jata hai. Yeh method overloading ya operator overloading ke through achieve hota hai.

`Method Overloading:` Jab ek hi method name ko multiple times declare kiya jata hai with different parameter lists (number or types of arguments), to usse compile-time polymorphism kehte hain.

Python mein method overloading ko directly support nahi kiya jata, kyunki Python mein functions ko dynamic arguments ke saath 
define kiya ja sakta hai. Lekin hum method overloading ka behavior achieve kar sakte hain using default arguments or variable-length 
arguments.


```python
class Display:
    def show(self, *args):
        if len(args) == 1:
            print(f"Displaying: {args[0]}")
        elif len(args) == 2:
            print(f"Displaying: {args[0]} and {args[1]}")

# Test
obj = Display()
obj.show("Hello")        # Displaying: Hello
obj.show("Hello", "World")  # Displaying: Hello and World


# Yahaan hum *args ka use kar rahe hain, jo ki method overloading ka behavior achieve karta hai.
```

###  Runtime Polymorphism (Dynamic Polymorphism)

Iska matlab hai ke polymorphism ko runtime ke dauran resolve kiya jata hai. Yeh method overriding ke through hota hai.

`Method Overriding:` Jab base class mein ek method hota hai aur derived class mein usi method ko override kiya jata hai, to runtime ke waqt jo method call hota hai, woh derived class ka hota hai, na ki base class ka.

Compile-time Polymorphism: Method overloading, Operator overloading.
Runtime Polymorphism: Method overriding.

    Aapka sawal bilkul valid hai! Lekin operator overriding ka concept actually C++ mein hi exist karta hai, aur yeh runtime polymorphism ke under nahi aata.


```python
class Animal:
    def sound(self):
        print("Animal makes a sound")

class Dog(Animal):
    def sound(self):
        print("Dog barks")

class Cat(Animal):
    def sound(self):
        print("Cat meows")

# Test
animals = [Dog(), Cat(), Animal()]

for animal in animals:
    animal.sound()  # Will call the appropriate overridden method


#Output:-
Dog barks
Cat meows
Animal makes a sound


Yahaan, runtime mein jab hum objects ko iterate karte hain, tab Python dynamic dispatch ke through correct sound() method call 
karta hai, jo ki derived class ka overridden method hota hai.
```

Yahan pe sound() method ko Animal, Dog, aur Cat classes mein define kiya gaya hai.
Polymorphism ke wajah se, jab hum sound() method ko call karte hain, toh wo alag-alag objects ke liye alag-alag output deta hai, depending on the type of object (Animal, Dog, or Cat).
Isse method overriding ka concept samajh mein aata hai, jisme subclass apne parent class ke method ko override karta hai apne specific implementation ke liye.

Compile-time Polymorphism (Method Overloading): Python mein hum argument types ko dynamically handle karke method overloading ka behavior achieve kar sakte hain.
Runtime Polymorphism (Method Overriding): Yeh Python mein directly inheritance aur method overriding ke through possible hota hai.

# Encapsulation 

Encapsulation Python mein ek object-oriented programming (OOP) concept hai, jisme data aur methods ko ek class ke andar bundle kiya jata hai. Matlab, ek object ki internal state ko hidden rakha jata hai, aur external world ko us object ke state ko access karne ke liye kuch controlled methods provide kiye jate hain.

Encapsulation ka matlab hai data ko chhupana aur access ko control karna.

Python mein, jab hum class banate hain, to uske andar ke data (variables) aur functions (methods) ko hum protect kar sakte hain.

Jab hum kisi object ko create karte hain, toh hum uske internal workings ko hide karte hain aur bas kuch specific methods provide karte hain, jisse bahar wale log us object ke saath interact kar sakein without knowing its internal details.

1. Data Hiding:- Class ke andar variables ko directly access karne se roka jata hai. Isse aap kisi object ke internal data ko directly modify nahi kar sakte. Sirf class ke methods ke through hi un data ko access kiya ja sakta hai.
Hum kisi class ke andar ke data ko directly access nahi karne dete, balki kuch specific functions ke through hi us data ko access karte hain.

2. Access Modifiers: Python mein aap variables aur methods ke access level ko control kar sakte hain.

Public: Ye variables aur methods koi bhi access kar sakta hai.
Private: Ye variables aur methods sirf class ke andar hi accessible hote hain. Ye variable ko _ (single underscore) ya __ (double underscore) laga ke banaya ja sakta hai.

Public aur private:
Public ka matlab hai wo data ya function koi bhi access kar sakta hai.
Private ka matlab hai wo data ya function sirf class ke andar hi use ho sakta hai, aur bahar se usko direct access nahi kiya ja sakta.


```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand     # Public data (sabko access kar sakte hain)
        self.__model = model   # Private data (sirf class ke andar access ho sakta hai)

    # Ye function private data ko access karne ka tarika hai
    def get_model(self):
        return self.__model

    def set_model(self, model):
        self.__model = model

# Car ka object banate hain
car1 = Car("Toyota", "Corolla")
print(car1.brand)          # Public data ko directly access kiya (output: Toyota)
print(car1.get_model())    # Private data ko function ke through access kiya (output: Corolla)

# Directly private data ko access nahi kar sakte
# print(car1.__model)     # Ye error dega

```

Public variables ko directly access kiya ja sakta hai (jaise car1.brand).
Private variables ko direct access nahi kar sakte. Unhe access karne ke liye hum methods (jaise get_model()) use karte hain.
Public variables can be accessed directly (like car1.brand).
Private variables (denoted with __ before the name) can only be accessed through methods like get_model() and set_model().

Encapsulation ka fayda yeh hai ki hum data ko protect kar sakte hain aur ensure kar sakte hain ki koi bhi galat tareeke se data ko change na kar de.

# Abstraction 

Python mein abstraction ek programming concept hai jisme hum kisi cheez ke implementation details ko hide kar dete hain aur sirf uske essential features ko show karte hain. Isse hum complex cheezon ko simplify kar paate hain.

Abstraction ka main purpose hai ki hum unnecessary details ko chhupa kar sirf relevant information dikhayein. Ye mostly classes aur methods mein hota hai.


```python
# Abstraction ko implement karne ke liye Python mein hum abstract classes aur abstract methods ka use karte hain. Iska example yeh hai:

from abc import ABC, abstractmethod

# Abstract class
class Animal(ABC):

    # Abstract method
    @abstractmethod
    def sound(self):
        pass

# Subclass
class Dog(Animal):
    
    # Implementing the abstract method
    def sound(self):
        return "Bark"

class Cat(Animal):
    
    # Implementing the abstract method
    def sound(self):
        return "Meow"

# Creating objects of Dog and Cat
dog = Dog()
cat = Cat()

# Calling the implemented method
print(dog.sound())  # Output: Bark
print(cat.sound())  # Output: Meow

```

Animal class ek abstract class hai jisme sound() method ko abstract declare kiya gaya hai.
Dog aur Cat classes mein sound() method ko implement kiya gaya hai, jo ke unke specific behavior ko define karte hain.
Jab hum Dog aur Cat ka object bana kar unka sound() method call karte hain, toh yeh unka specific behavior show karta hai

Abstraction ka fayda yeh hai ki hum bas yeh dekhte hain ki sound() method kis cheez ko represent karta hai, bina yeh jaane ki wo method internally kaise kaam kar raha hai.

# Constructor 

Python mein constructor ek special method hota hai jo ek class ka object create hone par automatically call hota hai. Iska main purpose class ke objects ko initialize karna (initialize karte waqt unki properties set karna) hota hai.


```python
class MyClass:
    def __init__(self, param1, param2):
        self.param1 = param1
        self.param2 = param2

# Yahan par __init__ method ko constructor ke roop mein jaana jaata hai. Jab bhi aap MyClass ka object banate hain,
# to __init__ method automatically call hota hai.
```


```python
# 1. Default Constructor: Jab constructor mein koi parameter nahi hota, ya parameters default values ke saath diye jaate hain.

class Demo:
    pass  # No constructor defined

obj = Demo()
```


```python
# 2. Parameterized Constructor: Jab constructor mein parameters diye jaate hain aur unke zariye object ko initialize kiya jaata hai.

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
# Parameterized Constructor hai — lekin default values ke sath

class Person:
    def __init__(self, name="Unknown", age=0):
        self.name = name
        self.age = age
```


```python
# 3. Non-parameterized Constructor:- Constructor me koi parameter nahi hota (sirf self hota hai).

class Demo:
    def __init__(self):
        print("Non-parameterized constructor")

obj = Demo()
```

`Constructor ka Important Role:`

Object Initialization: Constructor ka main role hota hai object ko initialize karna. Jab bhi koi object banaya jaata hai, usko kuch default values ya specific values assign ki jaati hain.

Memory Management: Constructor object creation ke time memory ko allocate karta hai, jisme uske attributes store kiye jaate hain.

Encapsulation: Constructor object ke properties ko initialize karke ek encapsulated environment create karta hai, jisme object ki internal details hidden hoti hain. Ye concept OOP (Object-Oriented Programming) ka ek part hai.

# <<<--- ThankYou   ---->>>
