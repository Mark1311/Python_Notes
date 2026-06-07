# Diff b/w List, tuple, set and Dict

| Feature                                 | **List**                                     | **Tuple**                  | **Set**                      | **Dictionary**                |
| --------------------------------------- | -------------------------------------------- | -------------------------- | ---------------------------- | ----------------------------- |
| Syntax                                  | `[]`                                         | `()`                       | `{}`                         | `{key: value}`                |
| Ordered                                 | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | ✔ Yes (Python 3.7+)           |
| Indexed                                 | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | Keys ke basis par             |
| Mutable (Change possible)               | ✔ Yes                                        | ❌ No (immutable)           | ✔ Yes                        | ✔ Yes                         |
| Duplicate Values Allowed                | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | ❌ Keys cannot repeat          |
| Heterogeneous Data (mixed data allowed) | ✔ Yes                                        | ✔ Yes                      | ✔ Yes                        | ✔ Yes                         |
| When to use                             | Values frequently change                     | Fixed collection of values | Unique items collection      | Key–value mapping             |
| Performance                             | Slowest (because mutable & index maintained) | Fast (immutable)           | Fast search & unique storage | Fast search via keys          |
| Example                                 | `[10, 20, 20, 30]`                           | `(10, 20, 30)`             | `{10, 20, 30}`               | `{"name": "Amit", "age": 25}` |


# f-string

Python me f-string ek aisa tareeka hai jisse hum string ke andar variables ko directly embed kar sakte hain — bina + concatenate kiye ya .format() use kiye.


```python
name = "Rahul"
age = 22

print(f"My name is {name} and I am {age} years old.")

#----------------------------------------------------------

a = 5
b = 3
print(f"Sum = {a + b}")

#-----------------------------------------------------------

name = "Amit"
marks = 92
print(f"""
Student: {name}
Marks: {marks}
Status: {"Pass" if marks > 40 else "Fail"}
""")
```

# 📌 Recursion in Python — Definition

Recursion ek aisa programming technique hai jisme function khud ko hi call karta hai problem solve karne ke liye.

→ Matlab function apne andar se again same function ko call kare, jab tak problem ka smallest part (base case) solve na ho jaye.


```python
# Factorial using Recursion

def factorial(n):
    if n == 1:                 # Base case
        return 1
    return n * factorial(n - 1)   # Recursive call

print(factorial(5))
```

    120
    

# 🔥 Docstring ko print kaise kare?


```python
def add(a, b):
    """This function returns the sum of two numbers"""
    return a + b

print(add.__doc__)

# --------------------------------

class Person:
    """This class is used to store person details"""
    pass

print(Person.__doc__)

```

    This function returns the sum of two numbers
    This class is used to store person details
    

# 📌 try, except aur finally kya hote hain?

| Block     | Purpose                                                         |
| --------- | --------------------------------------------------------------- |
| `try`     | Jisme error aane ka chance ho — risky code                      |
| `except`  | Error ko handle karta hai — program ko stop hone se bachata hai |
| `finally` | Hamesha chalega — chahe error ho ya na ho                       |



```python
#Example:-

try:
    num = int(input("Enter a number: "))
    print(10 / num)
except:
    print("Something went wrong!")
finally:
    print("Program Ended")
```

| Feature             | `try`                | `except`                        | `finally`                           |
| ------------------- | -------------------- | ------------------------------- | ----------------------------------- |
| Purpose             | Check / monitor code | Handle error                    | Cleanup / must-run code             |
| Error required?     | Error ho sakta hai   | Only chalata hai jab error aaye | Hamesha chalega (error ho ya na ho) |
| Optional / Required | Required             | Optional (but usually used)     | Optional                            |
| Runs when no error  | ✔ Yes                | ❌ No                            | ✔ Yes                               |
| Runs when error     | ❌ Stops at error     | ✔ Yes                           | ✔ Yes                               |


# ⚠ Important Interview Notes

✔ finally block exception ke baad bhi execute hota hai

✔ finally return statement ko bhi override kar sakta hai

✔ except multiple ho sakte hain, finally sirf ek hota hai

✔ try ke bina except allowed nahi, par try + finally allowed hai

# 📌 Scope (Space) kya hota hai?

Scope ka matlab variable kaha tak access ho sakta hai — yaani variable ki visibility (kahaan use kiya ja sakta hai).

| Scope Type       | Meaning                           |
| ---------------- | --------------------------------- |
| **Global Space** | Pure program me accessible        |
| **Local Space**  | Sirf function ke andar accessible |


# 🔹 Global Space (Global Scope)

Jo variable function ke bahar declare kiya jaata hai, wo global space me store hota hai
Aur pure program me use ho sakta hai.


```python
x = 10  # Global variable

def show():
    print(x)  # Accessing global variable

show()
print(x)  # Access outside function also

#Output
10
10
```

# 🔸 Local Space (Local Scope)

Jo variable function ke andar banaya jaata hai, wo sirf us function ke andar hi accessible hota hai


```python
def show():
    y = 5  # Local variable
    print(y)

show()
print(y)   # Error

#Output
5
NameError: name 'y' is not defined
```

# Dunder Methods (ya Magic Methods / Special Methods)

Python me Dunder Methods (ya Magic Methods / Special Methods) wo methods hote hain jinke naam ke aage aur peeche double underscore __ lagta hai.

`🔹 Dunder = Double + Under ( __ )`

Isliye inhe dunder methods bola jata hai.

### 📌 Definition

Dunder Methods aise predefined special methods hote hain jo Python classes ke objects ke behavior ko control karne ke liye use hote hain.
Ye methods automatically call hote hain, hume manually call nahi karna padta.

| Method       | Purpose / Kaam                                                 |
| ------------ | -------------------------------------------------------------- |
| `__init__()` | Object initialize karne ke liye (Constructor)                  |
| `__str__()`  | Print formatting decide karta hai (`print(obj)`) par call hota |
| `__repr__()` | Object ka developer representation deta hai                    |
| `__len__()`  | `len(obj)` ka response return karta hai                        |
| `__add__()`  | `+` operator ka behavior define karta hai                      |
| `__sub__()`  | `-` operator ka behavior define karta hai                      |
| `__mul__()`  | `*` operator ka behavior define karta hai                      |
| `__eq__()`   | Comparison `==` ka behavior define karta hai                   |
| `__del__()`  | Object destroy hone par call hota (Destructor)                 |



```python
#Example

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Name: {self.name}, Age: {self.age}"

p = Person("Bittu", 22)
print(p)
```

    Name: Bittu, Age: 22
    

# Walrus Operator

Python me Walrus Operator (:=) ek assignment expression operator hai jiska use value ko assign karne + use karne ke liye ek hi line me kiya jata hai.

### 📌 Definition

Walrus operator (:=) aisi value ko variable me assign karta hai jo expression ke beech me hi use ki ja rahi ho.
Matlab: value assign + expression evaluation ek saath.


```python
n = len("Python")
if n > 3:
    print(n)
```

    6
    


```python
if (n := len("Python")) > 3:
    print(n)
```

    6
    


```python
numbers = [10, 4, 25, 8, 15]

if (big := max(numbers)) > 20:
    print("Big Number:", big)

```

    Big Number: 25
    

# 🔶 Getter

### 📌 Getter kya hota hai?

Getter ek method hota hai jo private variable ki value ko read / access karne ke liye use hota hai.

Agar variable private hai (__variable) to usko class ke bahar direct access nahi kiya ja sakta.
Isliye Getter method ki help se value ko safely access kiya jata hai.

### Getter ka Rule

* Variable private hona chahiye (__name)
* Getter method value return karega (change nahi karega)


```python
class Person:
    def __init__(self, age):
        self.__age = age   # private variable

    def get_age(self):     # Getter method
        return self.__age

p = Person(22)
print(p.get_age())  # Getter ko call kiya
```

    22
    

#### ⚡ Getter kab use hota hai?

* ✔ Jab aap private data ko read karna chahte ho
* ❌ Lekin usko change nahi karna chahte

# 🔶 Setter 

### 📌 Setter kya hota hai?

Setter ek method hota hai jo private variable ki value ko update / change karne ke liye use hota hai.

Agar variable private hai (__variable) to class ke bahar se uski value direct change nahi ki ja sakti.
Isliye Setter method ki help se value ko safe tarike se modify kiya jata hai.

### 🧠 Setter ka Rule

* Variable private hona chahiye (__name)
* Setter method nayi value accept karega
* Setter method variable ko modify karega
* Validation (check) yahi par hoti hai
example: negative age, marks > 100, empty string etc.


```python
class Person:
    def __init__(self, age):
        self.__age = age    # private variable

    def set_age(self, new_age):   # Setter method
        if new_age > 0:
            self.__age = new_age
        else:
            print("Invalid age")
p = Person(22)

p.set_age(25)     # Age update hogi
p.set_age(-5)     # Invalid, setter value change nahi karega

```

    Invalid age
    

### ⚡ Setter kab use hota hai?

* ✔ Jab private variable ki value change karni ho
* ✔ Jab aap update se pehle validation lagana chahte ho
* ❌ Direct assign karna allowed nahi hota

`Summery:-` Setter method private variable ki value ko modify (update) karne ke liye use hota hai.
Yeh method new value receive karta hai aur update karne se pehle validation bhi laga
sakta hai. Setter encapsulation provide karta hai kyunki yeh data ko secure aur
controlled tariqe se change karne deta hai.


# 🔥 Python Internally Kaise Work Karti Hai?

Python ek High-Level Interpreted Language hai.
Matlab Python ka code direct machine language me convert nahi hota, balki step-by-step interpreter ke through execute hota hai.

### 🔹 Step 1: Source Code

Sabse pehle hum Python file likhte hain:

### 🔹 Step 2: Python Code → Bytecode

Interpreter pehla kaam karta hai:
   
    * Code ko Bytecode me convert karta hai
Bytecode file virtual machine ke liye hoti hai (machine code ke nahi)

### 🔹 Step 3: Bytecode → Python Virtual Machine (PVM)

Bytecode ko PVM (Python Virtual Machine) execute karta hai.

PVM:
* Step-by-step har instruction execute karta hai
* Execution ke dauran error handle karta hai

### 🔹 Step 4: Memory Management

Python execution ke dauran:

* Variables ko memory allocate hoti hai
* Objects ko track kiya jata hai
* Reference counting hota hai
➡ Garbage Collector memory free karta hai

### 🔹 Step 5: Output

Last me interpreter result show karta hai:

* Console me print
* Program completion

Your Code (.py)
        ↓
Bytecode (.pyc)
        ↓
Python Virtual Machine (PVM)
        ↓
Memory Management + Garbage Collection
        ↓
Final Output


          ┌────────────────────┐
          │   Python Source    │
          │    Code (.py)      │
          └─────────┬──────────┘
                    │
                    ▼
          ┌────────────────────┐
          │   Compilation to   │
          │  Bytecode (.pyc)   │
          │ (Created inside    │
          │  __pycache__)      │
          └─────────┬──────────┘
                    │
                    ▼
          ┌────────────────────┐
          │ Python Virtual     │
          │   Machine (PVM)    │
          │ Executes Bytecode  │
          └─────────┬──────────┘
                    │
                    ▼
      ┌────────────────────────────────┐
      │ Memory Management System       │
      │  • Object allocation           │
      │  • Reference Counting          │
      │  • Garbage Collector           │
      └─────────┬──────────────────────┘
                │
                ▼
          ┌────────────────────┐
          │   Final Output     │
          │ (Console / Screen) │
          └────────────────────┘


`Summery:- ` Python code sabse pehle bytecode (.pyc) me convert hota hai. Fir Python Virtual
Machine (PVM) bytecode ko line-by-line execute karta hai. Execution ke dauran 
Python memory manager variables ke liye memory allocate karta hai aur garbage 
collector unused objects ko delete karta hai. Final result console par show hota hai.

# Python compile language hai ya interpreted?

`Python dono hai — Compiled bhi aur Interpreted bhi.`

##### ✔ Kyon Python Compiled bhi hai?
Jab hum .py file run karte hain to Python pehle code ko compile karke Bytecode (.pyc file) banata hai.

* Source Code (.py)  →  Bytecode (.pyc)

Ye step Compiler ka kaam hai
(isliye Python compiled language bhi mani jaati hai)

##### ✔ Kyon Python Interpreted bhi hai?

Jo bytecode banta hai wo direct CPU execute nahi kar sakta, is bytecode ko Python Virtual Machine (PVM) line by line interpret karke chalata hai.

`Bytecode (.pyc)  →  PVM (Interpreter)  →  Output`

#### 🔥 Interview Point (Must Mention)

Python bytecode me compile hoti hai, fir PVM us bytecode ko interpret karke execute karta hai.
That's why Python is both a compiled and interpreted language.

`Summery:-` Python na to pure compiled language hai na hi pure interpreted language.
Python source code pehle bytecode (.pyc) me compile hota hai.
Fir bytecode ko Python Virtual Machine (PVM) line-by-line interpret karke
execute karti hai. Isliye Python compiled + interpreted language dono hai.

# Compile Language aur Interpreted Language

### 🔥 1️⃣ Compile Language (Compiled Language)

Compiled language me poora source code ek saath machine code me convert hota hai and phir execute hota hai.


```python
Source Code (.c / .cpp / .java
            ↓  Compiler
Machine Code (.exe / .obj)
            ↓
Execution
```

##### ⚡ Features

* ✔ Code ek hi baar translate hota hai
* ✔ Execution speed fast hoti hai
* ✔ Errors compile time par milte hain (run hone se pehle)

# 🔥 2️⃣ Interpreted Language

Interpreted language me source code line-by-line execute hota hai bina machine code me convert kiye.

#### ⚡ Features

* ✔ Execution time me flexibility
* ✔ Debugging easy
* ❌ Performance thodi slow compiled language ke comparison me
* Python, JavaScript, PHP, Ruby, Perl
Source Code (.py / .js / .php)
            ↓  Interpreter (line-by-line)
Execution
## 🔥 3️⃣ Difference Between Compiled vs Interpreted Languages

| Feature             | Compiled Language                      | Interpreted Language          |
| ------------------- | -------------------------------------- | ----------------------------- |
| Code Execution      | Full program ek saath convert hota hai | Line-by-line execute hota hai |
| Speed               | Fast                                   | Slow (line-by-line execution) |
| Error Detection     | Compile time pe detect                 | Runtime pe detect             |
| Output              | Executable file generate hoti hai      | Direct execution hota hai     |
| Platform Dependency | Mostly platform-dependent              | Mostly platform-independent   |
| Debugging           | Mushkil                                | Easy                          |
| Examples            | C, C++, Java, Rust                     | Python, JS, PHP, Ruby         |


# 🧵 Python String

Python me String ek sequence of characters hota hai.
    
String ko single quotes ' ', double quotes " " ya triple quotes ''' ''' se banaya ja sakta hai.


```python
s1 = 'Hello'
s2 = "Python"
s3 = '''Welcome to Programming'''
```


```python
# 1️⃣ upper() → String ko uppercase me convert karta hai

text = "python"
print(text.upper())   # PYTHON

# 2️⃣ lower() → String ko lowercase me convert karta hai

text = "HELLO"
print(text.lower())   # hello

# 3️⃣ title() → Har word ka first letter uppercase

text = "welcome to python"
print(text.title())   # Welcome To Python

# 4️⃣ capitalize() → Sirf first character uppercase

text = "python programming"
print(text.capitalize())   # Python programming

# 5️⃣ strip() → Start/end spaces hata deta hai

text = "   hello   "
print(text.strip())   # hello

# 6️⃣ replace(old, new) → Words replace karta hai

text = "I love Java"
print(text.replace("Java", "Python"))   # I love Python

# 7️⃣ split() → String ko list me convert karta hai

text = "a-b-c-d"
print(text.split("-"))   # ['a', 'b', 'c', 'd']

# 8️⃣ join() → List ke items ko string me convert karta hai

list1 = ["a", "b", "c"]
print("-".join(list1))   # a-b-c

# 9️⃣ find() → Substring position return karta hai (milne par index, nahi mila to -1)

text = "Python is awesome"
print(text.find("is"))   # 7

# 🔟 count() → Ek substring kitni baar aata hai

text = "banana"
print(text.count("a"))   # 3

# 1️⃣1️⃣ startswith() → True/False return (start check kare)

text = "python programming"
print(text.startswith("python"))   # True

# 1️⃣2️⃣ endswith() → True/False return (end check kare)

text = "hello world"
print(text.endswith("world"))   # True

# 1️⃣3️⃣ isdigit() → Check karta hai string sirf numbers hai ya nahi

text = "12345"
print(text.isdigit())   # True

# 1️⃣4️⃣ isalpha() → Check karta hai string sirf alphabets hai ya nahi

text = "Python"
print(text.isalpha())   # True

# 1️⃣5️⃣ isalnum() → Alphabet + numbers allowed (space nahi)

text = "Python123"
print(text.isalnum())   # True

# ⭐ Bonus — String Slicing (Bahut Important)

text = "PYTHON"
print(text[0:3])   # PYT
print(text[:4])    # PYTH
print(text[-3:])   # HON

```

# 📝 Python List

Python me List ek ordered, mutable (changeable) collection hoti hai, jisme multiple items (different data types) store kiye ja sakte hain.

`my_list = [10, "Hello", 3.5, True]`


```python
# 1️⃣ append() → List ke end me item add karta hai

nums = [1, 2, 3]
nums.append(4)
print(nums)   # [1, 2, 3, 4]

# 2️⃣ insert(index, value) → Specific position par value insert

nums = [10, 20, 30]
nums.insert(1, 15)
print(nums)   # [10, 15, 20, 30]

# 3️⃣ extend() → Ek list ke saath dusri list merge

a = [1, 2]
b = [3, 4]
a.extend(b)
print(a)   # [1, 2, 3, 4]

# 4️⃣ remove() → Value ko remove karta hai

nums = [1, 2, 3, 2]
nums.remove(2)
print(nums)   # [1, 3, 2]   (sirf first 2 remove hota hai)

# 5️⃣ pop() → Index ke base par element remove + return

nums = [10, 20, 30]
nums.pop(1)
print(nums)   # [10, 30]

# 6️⃣ clear() → Puri list empty

nums = [1, 2, 3]
nums.clear()
print(nums)   # []

# 7️⃣ index() → Value ka index return karta hai

nums = [5, 10, 15]
print(nums.index(10))   # 1

# 8️⃣ count() → Value kitni baar aayi hai

nums = [1, 2, 2, 3]
print(nums.count(2))   # 2

# 9️⃣ sort() → List ko ascending order me sort karta hai

nums = [4, 1, 3, 2]
nums.sort()
print(nums)   # [1, 2, 3, 4]

# 🔟 reverse() → List ko ulta kar deta hai

nums = [1, 2, 3]
nums.reverse()
print(nums)   # [3, 2, 1]

# ⭐ Bonus Concept — List Slicing (Bahut Important)

nums = [10, 20, 30, 40, 50]
print(nums[1:4])   # [20, 30, 40]
print(nums[:3])    # [10, 20, 30]
print(nums[-2:])   # [40, 50]

# ⭐ List Loop (Iteration)

nums = [10, 20, 30]
for n in nums:
    print(n)
```

# 📝 Python Tuple

Python me Tuple ek ordered, immutable (change-na-hone-wala) collection hota hai.
    
List jaisa hota hai, lekin tuple ko modify nahi kar sakte.

`my_tuple = (10, 20, 30, 40)`

* ✔ Indexing supported
* ✔ Duplicate values allowed
* ❌ Change / Add / Remove not allowed


```python
# 1️⃣ count() → Value kitni baar aayi hai

t = (1, 2, 2, 3)
print(t.count(2))   # 2

# 2️⃣ index() → Value ka index return

t = (10, 20, 30)
print(t.index(20))   # 1

# ⭐ Bonus — Tuple Slicing (List jaisa)

t = (10, 20, 30, 40, 50)
print(t[1:4])  # (20, 30, 40)
print(t[:3])   # (10, 20, 30)
print(t[-2:])  # (40, 50)


### 🔥 Tuple Packing & Unpacking (Bahut Important)
# 🎁 Packing

t = 10, 20, 30
print(t)   # (10, 20, 30)

# 📦 Unpacking

a, b, c = (10, 20, 30)
print(a, b, c)   # 10 20 30

# Single Element Tuple Important Note

t = (10,)   # Single element tuple
print(type(t))   # <class 'tuple'>
```


```python
# 1️⃣ How to Add Value in Tuple

### Tuple immutable hota hai, isliye direct add nahi kar sakte.
### But list me convert karke add kar sakte hain → phir tuple me convert.

t = (10, 20, 30)
temp = list(t)
temp.append(40)
t = tuple(temp)
print(t)   # (10, 20, 30, 40)

# 2️⃣ Tuple Slicing ===>  List jaisa hi slicing hota hai.

t = (10, 20, 30, 40, 50)
print(t[1:4])   # (20, 30, 40)
print(t[:3])    # (10, 20, 30)
print(t[-2:])   # (40, 50)

# 3️⃣ Value Get (Indexing) ===>  Specific position ki value lene ke liye index use.

t = (5, 10, 15, 20)
print(t[2])   # 15
print(t[-1])  # 20

# 4️⃣ Concatenation (2 Tuples Ko Jodna)   ===>>>  + operator se 2 tuples ko combine kar sakte hain.

t1 = (1, 2, 3)
t2 = (4, 5)
t3 = t1 + t2
print(t3)   # (1, 2, 3, 4, 5)

# 5️⃣ Remove Value from Tuple

# Direct remove nahi hota, kyunki tuple immutable hai.
# But list ke through trick se remove kar sakte hain:

t = (10, 20, 30, 20)
temp = list(t)
temp.remove(20)  # first 20 remove
t = tuple(temp)
print(t)   # (10, 30, 20)

# 6️⃣ del — Tuple Delete ===>> del se poora tuple delete ho jata hai, element delete nahi hota.

t = (10, 20, 30)
del t
print(t)   # ❌ Error — tuple does not exist

# 7️⃣ join() — Important Clarification

# 👉 join() tuple ka method nahi hota
# join actually string method hota hai jo tuple ke strings ko join karta hai.

t = ("A", "B", "C")
result = "-".join(t)
print(result)   # A-B-C
```

# ⭐ Difference Between List and Tuple (Quick Revision)

| Feature  | List                  | Tuple                   |
| -------- | --------------------- | ----------------------- |
| Syntax   | `[ ]`                 | `( )`                   |
| Mutable  | Yes                   | No                      |
| Speed    | Slow                  | Fast                    |
| Methods  | More                  | Very few                |
| Use Case | Data change hota rahe | Data fixed hona chahiye |


# 📝 Python Set

Python me Set ek unordered, unindexed, mutable collection hota hai jisme duplicate values allowed nahi hoti.

`my_set = {10, 20, 30, 40}`


```python
# 1️⃣ add() — Set me new value add karna

s = {1, 2, 3}
s.add(4)
print(s)   # {1, 2, 3, 4}

# 2️⃣ update() — Multiple values add / merge

s = {1, 2}
s.update([3, 4, 5])
print(s)   # {1, 2, 3, 4, 5}

# 3️⃣ remove() — Value remove but nahi mili to error

s = {10, 20, 30}
s.remove(20)
print(s)   # {10, 30}

# 4️⃣ discard() — Value remove karta par error nahi deta

s = {10, 20, 30}
s.discard(40)
print(s)   # {10, 20, 30}

# 5️⃣ pop() — Random element remove + return

s = {1, 2, 3}
item = s.pop()
print(item)  # Random element
print(s)

# 6️⃣ clear() — Set empty

s = {1, 2, 3}
s.clear()
print(s)   # set()

# ✔ union() → Sare unique values (OR operation)

a = {1, 2, 3}
b = {3, 4, 5}
print(a.union(b))   # {1, 2, 3, 4, 5}

# ✔ intersection() → Common values (AND operation)

a = {1, 2, 3}
b = {2, 3, 4}
print(a.intersection(b))   # {2, 3}

# ✔ difference() → a me jo hain but b me nahi

a = {1, 2, 3}
b = {2, 3}
print(a.difference(b))   # {1}

# ✔ symmetric_difference() → Unique in both (XOR)

a = {1, 2, 3}
b = {3, 4}
print(a.symmetric_difference(b))   # {1, 2, 4}

# 🎁 Check Membership — in keyword

s = {10, 20, 30}
print(20 in s)   # True
print(50 in s)   # False
```

# 📝 Python Dictionary

Python me Dictionary ek unordered, mutable collection hota hai jo key–value pairs ke form me data store karta hai.

`student = {"name": "Rahul", "age": 20, "city": "Delhi"}`


```python
# 1️⃣ get() → Key ki value safely return karta hai

d = {"name": "Aman", "age": 22}
print(d.get("age"))         # 22
print(d.get("city"))        # None (Error nahi deta)

# 2️⃣ keys() → Saare keys return

d = {"a": 1, "b": 2}
print(d.keys())    # dict_keys(['a', 'b'])

# 3️⃣ values() → Saari values return

d = {"a": 1, "b": 2}
print(d.values())   # dict_values([1, 2])

# 4️⃣ items() → Key + Value pair return

d = {"a": 1, "b": 2}
print(d.items())    # dict_items([('a', 1), ('b', 2)])

# 5️⃣ update() → Dictionary me value update / add

d = {"a": 1, "b": 2}
d.update({"b": 20, "c": 30})
print(d)    # {'a': 1, 'b': 20, 'c': 30}

# 6️⃣ pop() → Specific key remove + value return

d = {"a": 1, "b": 2, "c": 3}
d.pop("b")
print(d)    # {'a': 1, 'c': 3}

# 7️⃣ popitem() → Last inserted key–value hatata + return

d = {"a": 1, "b": 2, "c": 3}
d.popitem()
print(d)    # {'a': 1, 'b': 2}

# 8️⃣ clear() → Puri dictionary empty

d = {"x": 10, "y": 20}
d.clear()
print(d)   # {}

# 9️⃣ fromkeys() → Keys ke base par dict create

keys = ["a", "b", "c"]
d = dict.fromkeys(keys, 0)
print(d)   # {'a': 0, 'b': 0, 'c': 0}

#🔥 Dictionary — Add / Update / Remove Shortcut

#✔ Add

d = {"x": 1}
d["y"] = 2
print(d)   # {'x': 1, 'y': 2}

# ✔ Update value

d["x"] = 100
print(d)   # {'x': 100, 'y': 2}

# ✔ Delete key

del d["y"]
print(d)   # {'x': 100}

# ⭐ Loop Dictionary

d = {"name": "Rohan", "age": 21}

for key in d:
    print(key, d[key])
```

    22
    None
    dict_keys(['a', 'b'])
    dict_values([1, 2])
    dict_items([('a', 1), ('b', 2)])
    {'a': 1, 'b': 20, 'c': 30}
    {'a': 1, 'c': 3}
    {'a': 1, 'b': 2}
    {}
    {'a': 0, 'b': 0, 'c': 0}
    {'x': 1, 'y': 2}
    {'x': 100, 'y': 2}
    {'x': 100}
    name Rohan
    age 21
    

# Argument vs Parameter Python

## 🔷 Parameter (Function Definition ke Time)

📌 Parameter wo variable hote hain **jo function define karte waqt likhe jaate hain**. 

Ye input receive karne ke placeholder hote hain.

🔹 Parameter = Function ke andar data receive karne ke liye naam

### Example
```python
def add(a, b):   # a and b = parameters
    return a + b
```
## 🔷 Argument (Function Call ke Time)

📌 Argument wo real values hoti hain jo function ko call karte waqt pass ki jati hain.

```python
result = add(5, 10)   # 5 and 10 = arguments


| Feature          | Parameter                  | Argument                 |
| ---------------- | -------------------------- | ------------------------ |
| Kab use hota hai | Function define karte waqt | Function call karte waqt |
| Kya hota hai     | Variable name              | Actual value             |
| Position         | Function header            | Function calling         |
| Example          | `a, b`                     | `5, 10`                  |


`Parameter` = Function ke andar input receive karne ka placeholder,

`Argument` = Function ko call karte waqt diya gaya actual data

```

# 🔥 async & await Python

Python me jab hame asynchronous programming karni hoti hai (yaani code parallel tarike se chalana without blocking the program), tab async & await use hota hai.

Normally Python code step by step chalta hai:

`Step 1 → Step 2 → Step 3 ...`

Lekin asynchronous code me multiple tasks ek sath chal sakte hain, jisse program fast ho jata hai — specially jab network request, database call, file download jaisi slow operations ho.

## 📌 async ka matlab

async ka use function ko asynchronous function banane ke liye hota hai.

```py
`async def my_function():
    ...
```

## 📌 await ka matlab

await ka use async function ke andar hota hai, jab hum kisi asynchronous task ke complete hone ka wait karte hain — bina pura program ko block kiye.

```py
    await some_async_task()
```


```python
## Example

import asyncio

async def download_file():
    print("Download started...")
    await asyncio.sleep(3)   # ye 3 seconds wait karega but program block nahi hoga
    print("Download complete!")

async def main():
    await download_file()

asyncio.run(main())

```


```python
# Example

import asyncio

async def task1():
    print("Task 1 started")
    await asyncio.sleep(3)
    print("Task 1 done")

async def task2():
    print("Task 2 started")
    await asyncio.sleep(2)
    print("Task 2 done")

async def main():
    await asyncio.gather(task1(), task2())

asyncio.run(main())

```


```python
#Output
Task 1 started
Task 2 started
(wait 2 sec)
Task 2 done
(wait 1 sec)
Task 1 done
```

# 🔥 Asynchronous Programming


### Normal programming (Synchronous)

Jab program ek line complete hone ke baad hi next line chalata hai.
`Task 1 → Task 2 → Task 3`

Agar Task 1 slow hai (jaise network request / database / file download), to purā program ruk jata hai us task ke complete hone ka wait karte hue.


### Asynchronous programming

Isme program slow task ke complete hone ka wait nahi karta, balki jab tak wo slow task complete ho, tab tak baaki tasks parallel me chalte rehte hain.

```python
Task 1 (slow) ────────────▶
Task 2 ──▶
Task 3 ──▶
```


```python
### 🧠 Simple Python Example Compare

##### ❌ Synchronous (Slow)

download_file()  # 5 sec
send_email()     # 3 sec
log_report()     # 2 sec

Total time = 5 + 3 + 2 = 10 sec

##### ✔ Asynchronous (Fast)

download_file() 5 sec
send_email()    3 sec
log_report()    2 sec


Teeno same time pe start hote hain
Total time = max(5, 3, 2) = 5 sec only
```

# UseCase

| Task Type                   | Best Approach                                 |
| --------------------------- | --------------------------------------------- |
| Network request (API calls) | Async                                         |
| Database queries            | Async                                         |
| Emails sending              | Async                                         |
| Files download/uploads      | Async                                         |
| Heavy CPU calculations      | Async nahi — multiprocessing/threading better |



# Match Case in Python

## Match Case Kya Hota Hai?

`match-case` Python ka ek **pattern matching statement** hai jo Python 3.10 me introduce hua tha.

Ye bahut had tak dusri programming languages ke **switch-case** statement jaisa kaam karta hai.

Iska use multiple conditions ko clean aur readable way me handle karne ke liye kiya jata hai.

---

## Syntax

```python
match variable:
    case value1:
        # code
    case value2:
        # code
    case _:
        # default code
```

---

## Simple Example

```python
day = 2

match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Invalid Day")
```

### Output

```text
Tuesday
```

---

## case _ Kya Hota Hai?

`_` default case hota hai.

Agar koi bhi condition match nahi hoti to ye execute hota hai.

```python
number = 10

match number:
    case 1:
        print("One")
    case 2:
        print("Two")
    case _:
        print("Unknown Number")
```

### Output

```text
Unknown Number
```

---

## Multiple Values Match Karna

```python
status = 400

match status:
    case 200:
        print("Success")
    case 400 | 401 | 403:
        print("Client Error")
    case 500:
        print("Server Error")
```

### Output

```text
Client Error
```

---

## Match Case vs If-Else

### Using If-Else

```python
day = 2

if day == 1:
    print("Monday")
elif day == 2:
    print("Tuesday")
elif day == 3:
    print("Wednesday")
else:
    print("Invalid Day")
```

### Using Match Case

```python
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Invalid Day")
```

`match-case` code ko jyada readable aur clean bana deta hai jab bahut saari conditions ho.

---

## Advantages

- Code readable hota hai.
- Multiple conditions easily handle hoti hain.
- Switch-case jaisa syntax milta hai.
- Complex pattern matching support karta hai.

---

## Important Points

- Python 3.10+ me available hai.
- `switch-case` ka alternative mana jata hai.
- Default case ke liye `_` use kiya jata hai.
- Pattern matching support karta hai.

---

## Interview Answer (Short)

**Match-case Python 3.10 me introduce hua ek pattern matching statement hai jo switch-case ki tarah kaam karta hai. Iska use multiple conditions ko clean aur readable way me handle karne ke liye kiya jata hai. Default case ke liye `_` use hota hai.**

# File Handling in Python

File Handling ek process hai jiske through Python program files ke saath interact karta hai.

Iski help se hum file me stored data ko access, manage aur modify kar sakte hain. File system me maujood data ko program ke andar use karne ke liye file handling ka use kiya jata hai.

---

## Writing Data into a File

```python
file = open("student.txt", "w")

file.write("My name is Bittu")
file.close()
```

### Explanation

- `open()` file ko open karta hai.
- `"w"` mode file me data write karne ke liye use hota hai.
- `write()` file me data save karta hai.
- `close()` file ko close karta hai.

---

## Reading Data from a File

```python
file = open("student.txt", "r")

data = file.read()
print(data)

file.close()
```

### Explanation

- `"r"` mode file ko read karne ke liye use hota hai.
- `read()` file ka pura content read karta hai.
- `print()` content ko screen par display karta hai.
- `close()` file ko close karta hai.

---

# Difference Between readline() and writelines() in Python

## readline()

`readline()` ka use file se **ek time par sirf ek line** read karne ke liye kiya jata hai.

### Example

File Content (`student.txt`)

```text
Bittu
Rahul
Aman
```

```python
file = open("student.txt", "r")

line1 = file.readline()
line2 = file.readline()

print(line1)
print(line2)

file.close()
```

### Output

```text
Bittu

Rahul
```

### Explanation

- Pehli `readline()` first line read karegi.
- Dusri `readline()` second line read karegi.
- Har call next line par move ho jati hai.

---

## writelines()

`writelines()` ka use ek saath multiple lines ko file me write karne ke liye kiya jata hai.

### Example

```python
file = open("student.txt", "w")

data = [
    "Bittu\n",
    "Rahul\n",
    "Aman\n"
]

file.writelines(data)

file.close()
```

### File Content After Execution

```text
Bittu
Rahul
Aman
```

### Explanation

- `writelines()` list ya iterable ko accept karta hai.
- List ke saare elements file me write ho jate hain.
- `writelines()` automatically new line (`\n`) add nahi karta, hume khud dena padta hai.

---

## readline() vs writelines()

| readline() | writelines() |
|------------|-------------|
| File se data read karta hai | File me data write karta hai |
| Ek baar me ek line read karta hai | Ek baar me multiple lines write karta hai |
| Read operation hai | Write operation hai |
| Mostly `"r"` mode ke saath use hota hai | Mostly `"w"` ya `"a"` mode ke saath use hota hai |

---

## Interview Answer (Short)

**`readline()` file se ek time par ek line read karne ke liye use hota hai, jabki `writelines()` multiple lines ko ek saath file me write karne ke liye use hota hai. `writelines()` automatic newline add nahi karta, isliye `\n` manually dena padta hai.**


# tell(), seek() and truncate() in Python

## tell()

`tell()` current file cursor (pointer) ki position batata hai.

### Example

```python
file = open("student.txt", "r")

print(file.tell())

file.read(5)

print(file.tell())

file.close()
```

### Output

```text
0
5
```

### Explanation

- Starting me cursor position `0` hoti hai.
- 5 characters read karne ke baad cursor position `5` ho jati hai.

---

## seek()

`seek()` cursor ko kisi specific position par le jane ke liye use hota hai.

### Example

```python
file = open("student.txt", "r")

file.seek(3)

print(file.read())

file.close()
```

### File Content

```text
Bittu
```

### Output

```text
tu
```

### Explanation

- `seek(3)` cursor ko 3rd index par le gaya.
- Read wahin se start hua.

---

## truncate()

`truncate()` file ke content ko specified size tak cut kar deta hai.

### Example

```python
file = open("student.txt", "r+")

file.truncate(5)

file.close()
```

### Before

```text
Bittu Kumar
```

### After

```text
Bittu
```

### Explanation

- `truncate(5)` sirf pehle 5 characters rakhega.
- Baaki content remove ho jayega.

---

## Interview Answer (Short)

- **tell()** → Current cursor position batata hai.
- **seek()** → Cursor ko specific position par le jata hai.
=======
# Diff b/w List, tuple, set and Dict

| Feature                                 | **List**                                     | **Tuple**                  | **Set**                      | **Dictionary**                |
| --------------------------------------- | -------------------------------------------- | -------------------------- | ---------------------------- | ----------------------------- |
| Syntax                                  | `[]`                                         | `()`                       | `{}`                         | `{key: value}`                |
| Ordered                                 | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | ✔ Yes (Python 3.7+)           |
| Indexed                                 | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | Keys ke basis par             |
| Mutable (Change possible)               | ✔ Yes                                        | ❌ No (immutable)           | ✔ Yes                        | ✔ Yes                         |
| Duplicate Values Allowed                | ✔ Yes                                        | ✔ Yes                      | ❌ No                         | ❌ Keys cannot repeat          |
| Heterogeneous Data (mixed data allowed) | ✔ Yes                                        | ✔ Yes                      | ✔ Yes                        | ✔ Yes                         |
| When to use                             | Values frequently change                     | Fixed collection of values | Unique items collection      | Key–value mapping             |
| Performance                             | Slowest (because mutable & index maintained) | Fast (immutable)           | Fast search & unique storage | Fast search via keys          |
| Example                                 | `[10, 20, 20, 30]`                           | `(10, 20, 30)`             | `{10, 20, 30}`               | `{"name": "Amit", "age": 25}` |


# f-string

Python me f-string ek aisa tareeka hai jisse hum string ke andar variables ko directly embed kar sakte hain — bina + concatenate kiye ya .format() use kiye.


```python
name = "Rahul"
age = 22

print(f"My name is {name} and I am {age} years old.")

#----------------------------------------------------------

a = 5
b = 3
print(f"Sum = {a + b}")

#-----------------------------------------------------------

name = "Amit"
marks = 92
print(f"""
Student: {name}
Marks: {marks}
Status: {"Pass" if marks > 40 else "Fail"}
""")
```

# 📌 Recursion in Python — Definition

Recursion ek aisa programming technique hai jisme function khud ko hi call karta hai problem solve karne ke liye.

→ Matlab function apne andar se again same function ko call kare, jab tak problem ka smallest part (base case) solve na ho jaye.


```python
# Factorial using Recursion

def factorial(n):
    if n == 1:                 # Base case
        return 1
    return n * factorial(n - 1)   # Recursive call

print(factorial(5))
```

    120
    

# 🔥 Docstring ko print kaise kare?


```python
def add(a, b):
    """This function returns the sum of two numbers"""
    return a + b

print(add.__doc__)

# --------------------------------

class Person:
    """This class is used to store person details"""
    pass

print(Person.__doc__)

```

    This function returns the sum of two numbers
    This class is used to store person details
    

# 📌 try, except aur finally kya hote hain?

| Block     | Purpose                                                         |
| --------- | --------------------------------------------------------------- |
| `try`     | Jisme error aane ka chance ho — risky code                      |
| `except`  | Error ko handle karta hai — program ko stop hone se bachata hai |
| `finally` | Hamesha chalega — chahe error ho ya na ho                       |



```python
#Example:-

try:
    num = int(input("Enter a number: "))
    print(10 / num)
except:
    print("Something went wrong!")
finally:
    print("Program Ended")
```

| Feature             | `try`                | `except`                        | `finally`                           |
| ------------------- | -------------------- | ------------------------------- | ----------------------------------- |
| Purpose             | Check / monitor code | Handle error                    | Cleanup / must-run code             |
| Error required?     | Error ho sakta hai   | Only chalata hai jab error aaye | Hamesha chalega (error ho ya na ho) |
| Optional / Required | Required             | Optional (but usually used)     | Optional                            |
| Runs when no error  | ✔ Yes                | ❌ No                            | ✔ Yes                               |
| Runs when error     | ❌ Stops at error     | ✔ Yes                           | ✔ Yes                               |


# ⚠ Important Interview Notes

✔ finally block exception ke baad bhi execute hota hai

✔ finally return statement ko bhi override kar sakta hai

✔ except multiple ho sakte hain, finally sirf ek hota hai

✔ try ke bina except allowed nahi, par try + finally allowed hai

# 📌 Scope (Space) kya hota hai?

Scope ka matlab variable kaha tak access ho sakta hai — yaani variable ki visibility (kahaan use kiya ja sakta hai).

| Scope Type       | Meaning                           |
| ---------------- | --------------------------------- |
| **Global Space** | Pure program me accessible        |
| **Local Space**  | Sirf function ke andar accessible |


# 🔹 Global Space (Global Scope)

Jo variable function ke bahar declare kiya jaata hai, wo global space me store hota hai
Aur pure program me use ho sakta hai.


```python
x = 10  # Global variable

def show():
    print(x)  # Accessing global variable

show()
print(x)  # Access outside function also

#Output
10
10
```

# 🔸 Local Space (Local Scope)

Jo variable function ke andar banaya jaata hai, wo sirf us function ke andar hi accessible hota hai


```python
def show():
    y = 5  # Local variable
    print(y)

show()
print(y)   # Error

#Output
5
NameError: name 'y' is not defined
```

# Dunder Methods (ya Magic Methods / Special Methods)

Python me Dunder Methods (ya Magic Methods / Special Methods) wo methods hote hain jinke naam ke aage aur peeche double underscore __ lagta hai.

`🔹 Dunder = Double + Under ( __ )`

Isliye inhe dunder methods bola jata hai.

### 📌 Definition

Dunder Methods aise predefined special methods hote hain jo Python classes ke objects ke behavior ko control karne ke liye use hote hain.
Ye methods automatically call hote hain, hume manually call nahi karna padta.

| Method       | Purpose / Kaam                                                 |
| ------------ | -------------------------------------------------------------- |
| `__init__()` | Object initialize karne ke liye (Constructor)                  |
| `__str__()`  | Print formatting decide karta hai (`print(obj)`) par call hota |
| `__repr__()` | Object ka developer representation deta hai                    |
| `__len__()`  | `len(obj)` ka response return karta hai                        |
| `__add__()`  | `+` operator ka behavior define karta hai                      |
| `__sub__()`  | `-` operator ka behavior define karta hai                      |
| `__mul__()`  | `*` operator ka behavior define karta hai                      |
| `__eq__()`   | Comparison `==` ka behavior define karta hai                   |
| `__del__()`  | Object destroy hone par call hota (Destructor)                 |



```python
#Example

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Name: {self.name}, Age: {self.age}"

p = Person("Bittu", 22)
print(p)
```

    Name: Bittu, Age: 22
    

# Walrus Operator

Python me Walrus Operator (:=) ek assignment expression operator hai jiska use value ko assign karne + use karne ke liye ek hi line me kiya jata hai.

### 📌 Definition

Walrus operator (:=) aisi value ko variable me assign karta hai jo expression ke beech me hi use ki ja rahi ho.
Matlab: value assign + expression evaluation ek saath.


```python
n = len("Python")
if n > 3:
    print(n)
```

    6
    


```python
if (n := len("Python")) > 3:
    print(n)
```

    6
    


```python
numbers = [10, 4, 25, 8, 15]

if (big := max(numbers)) > 20:
    print("Big Number:", big)

```

    Big Number: 25
    

# 🔶 Getter

### 📌 Getter kya hota hai?

Getter ek method hota hai jo private variable ki value ko read / access karne ke liye use hota hai.

Agar variable private hai (__variable) to usko class ke bahar direct access nahi kiya ja sakta.
Isliye Getter method ki help se value ko safely access kiya jata hai.

### Getter ka Rule

* Variable private hona chahiye (__name)
* Getter method value return karega (change nahi karega)


```python
class Person:
    def __init__(self, age):
        self.__age = age   # private variable

    def get_age(self):     # Getter method
        return self.__age

p = Person(22)
print(p.get_age())  # Getter ko call kiya
```

    22
    

#### ⚡ Getter kab use hota hai?

* ✔ Jab aap private data ko read karna chahte ho
* ❌ Lekin usko change nahi karna chahte

# 🔶 Setter 

### 📌 Setter kya hota hai?

Setter ek method hota hai jo private variable ki value ko update / change karne ke liye use hota hai.

Agar variable private hai (__variable) to class ke bahar se uski value direct change nahi ki ja sakti.
Isliye Setter method ki help se value ko safe tarike se modify kiya jata hai.

### 🧠 Setter ka Rule

* Variable private hona chahiye (__name)
* Setter method nayi value accept karega
* Setter method variable ko modify karega
* Validation (check) yahi par hoti hai
example: negative age, marks > 100, empty string etc.


```python
class Person:
    def __init__(self, age):
        self.__age = age    # private variable

    def set_age(self, new_age):   # Setter method
        if new_age > 0:
            self.__age = new_age
        else:
            print("Invalid age")
p = Person(22)

p.set_age(25)     # Age update hogi
p.set_age(-5)     # Invalid, setter value change nahi karega

```

    Invalid age
    

### ⚡ Setter kab use hota hai?

* ✔ Jab private variable ki value change karni ho
* ✔ Jab aap update se pehle validation lagana chahte ho
* ❌ Direct assign karna allowed nahi hota

`Summery:-` Setter method private variable ki value ko modify (update) karne ke liye use hota hai.
Yeh method new value receive karta hai aur update karne se pehle validation bhi laga
sakta hai. Setter encapsulation provide karta hai kyunki yeh data ko secure aur
controlled tariqe se change karne deta hai.


# 🔥 Python Internally Kaise Work Karti Hai?

Python ek High-Level Interpreted Language hai.
Matlab Python ka code direct machine language me convert nahi hota, balki step-by-step interpreter ke through execute hota hai.

### 🔹 Step 1: Source Code

Sabse pehle hum Python file likhte hain:

### 🔹 Step 2: Python Code → Bytecode

Interpreter pehla kaam karta hai:
   
    * Code ko Bytecode me convert karta hai
Bytecode file virtual machine ke liye hoti hai (machine code ke nahi)

### 🔹 Step 3: Bytecode → Python Virtual Machine (PVM)

Bytecode ko PVM (Python Virtual Machine) execute karta hai.

PVM:
* Step-by-step har instruction execute karta hai
* Execution ke dauran error handle karta hai

### 🔹 Step 4: Memory Management

Python execution ke dauran:

* Variables ko memory allocate hoti hai
* Objects ko track kiya jata hai
* Reference counting hota hai
➡ Garbage Collector memory free karta hai

### 🔹 Step 5: Output

Last me interpreter result show karta hai:

* Console me print
* Program completion

Your Code (.py)
        ↓
Bytecode (.pyc)
        ↓
Python Virtual Machine (PVM)
        ↓
Memory Management + Garbage Collection
        ↓
Final Output


          ┌────────────────────┐
          │   Python Source    │
          │    Code (.py)      │
          └─────────┬──────────┘
                    │
                    ▼
          ┌────────────────────┐
          │   Compilation to   │
          │  Bytecode (.pyc)   │
          │ (Created inside    │
          │  __pycache__)      │
          └─────────┬──────────┘
                    │
                    ▼
          ┌────────────────────┐
          │ Python Virtual     │
          │   Machine (PVM)    │
          │ Executes Bytecode  │
          └─────────┬──────────┘
                    │
                    ▼
      ┌────────────────────────────────┐
      │ Memory Management System       │
      │  • Object allocation           │
      │  • Reference Counting          │
      │  • Garbage Collector           │
      └─────────┬──────────────────────┘
                │
                ▼
          ┌────────────────────┐
          │   Final Output     │
          │ (Console / Screen) │
          └────────────────────┘


`Summery:- ` Python code sabse pehle bytecode (.pyc) me convert hota hai. Fir Python Virtual
Machine (PVM) bytecode ko line-by-line execute karta hai. Execution ke dauran 
Python memory manager variables ke liye memory allocate karta hai aur garbage 
collector unused objects ko delete karta hai. Final result console par show hota hai.

# Python compile language hai ya interpreted?

`Python dono hai — Compiled bhi aur Interpreted bhi.`

##### ✔ Kyon Python Compiled bhi hai?
Jab hum .py file run karte hain to Python pehle code ko compile karke Bytecode (.pyc file) banata hai.

* Source Code (.py)  →  Bytecode (.pyc)

Ye step Compiler ka kaam hai
(isliye Python compiled language bhi mani jaati hai)

##### ✔ Kyon Python Interpreted bhi hai?

Jo bytecode banta hai wo direct CPU execute nahi kar sakta, is bytecode ko Python Virtual Machine (PVM) line by line interpret karke chalata hai.

`Bytecode (.pyc)  →  PVM (Interpreter)  →  Output`

#### 🔥 Interview Point (Must Mention)

Python bytecode me compile hoti hai, fir PVM us bytecode ko interpret karke execute karta hai.
That's why Python is both a compiled and interpreted language.

`Summery:-` Python na to pure compiled language hai na hi pure interpreted language.
Python source code pehle bytecode (.pyc) me compile hota hai.
Fir bytecode ko Python Virtual Machine (PVM) line-by-line interpret karke
execute karti hai. Isliye Python compiled + interpreted language dono hai.

# Compile Language aur Interpreted Language

### 🔥 1️⃣ Compile Language (Compiled Language)

Compiled language me poora source code ek saath machine code me convert hota hai and phir execute hota hai.


```python
Source Code (.c / .cpp / .java
            ↓  Compiler
Machine Code (.exe / .obj)
            ↓
Execution
```

##### ⚡ Features

* ✔ Code ek hi baar translate hota hai
* ✔ Execution speed fast hoti hai
* ✔ Errors compile time par milte hain (run hone se pehle)

# 🔥 2️⃣ Interpreted Language

Interpreted language me source code line-by-line execute hota hai bina machine code me convert kiye.

#### ⚡ Features

* ✔ Execution time me flexibility
* ✔ Debugging easy
* ❌ Performance thodi slow compiled language ke comparison me
* Python, JavaScript, PHP, Ruby, Perl
Source Code (.py / .js / .php)
            ↓  Interpreter (line-by-line)
Execution
## 🔥 3️⃣ Difference Between Compiled vs Interpreted Languages

| Feature             | Compiled Language                      | Interpreted Language          |
| ------------------- | -------------------------------------- | ----------------------------- |
| Code Execution      | Full program ek saath convert hota hai | Line-by-line execute hota hai |
| Speed               | Fast                                   | Slow (line-by-line execution) |
| Error Detection     | Compile time pe detect                 | Runtime pe detect             |
| Output              | Executable file generate hoti hai      | Direct execution hota hai     |
| Platform Dependency | Mostly platform-dependent              | Mostly platform-independent   |
| Debugging           | Mushkil                                | Easy                          |
| Examples            | C, C++, Java, Rust                     | Python, JS, PHP, Ruby         |


# 🧵 Python String

Python me String ek sequence of characters hota hai.
    
String ko single quotes ' ', double quotes " " ya triple quotes ''' ''' se banaya ja sakta hai.


```python
s1 = 'Hello'
s2 = "Python"
s3 = '''Welcome to Programming'''
```


```python
# 1️⃣ upper() → String ko uppercase me convert karta hai

text = "python"
print(text.upper())   # PYTHON

# 2️⃣ lower() → String ko lowercase me convert karta hai

text = "HELLO"
print(text.lower())   # hello

# 3️⃣ title() → Har word ka first letter uppercase

text = "welcome to python"
print(text.title())   # Welcome To Python

# 4️⃣ capitalize() → Sirf first character uppercase

text = "python programming"
print(text.capitalize())   # Python programming

# 5️⃣ strip() → Start/end spaces hata deta hai

text = "   hello   "
print(text.strip())   # hello

# 6️⃣ replace(old, new) → Words replace karta hai

text = "I love Java"
print(text.replace("Java", "Python"))   # I love Python

# 7️⃣ split() → String ko list me convert karta hai

text = "a-b-c-d"
print(text.split("-"))   # ['a', 'b', 'c', 'd']

# 8️⃣ join() → List ke items ko string me convert karta hai

list1 = ["a", "b", "c"]
print("-".join(list1))   # a-b-c

# 9️⃣ find() → Substring position return karta hai (milne par index, nahi mila to -1)

text = "Python is awesome"
print(text.find("is"))   # 7

# 🔟 count() → Ek substring kitni baar aata hai

text = "banana"
print(text.count("a"))   # 3

# 1️⃣1️⃣ startswith() → True/False return (start check kare)

text = "python programming"
print(text.startswith("python"))   # True

# 1️⃣2️⃣ endswith() → True/False return (end check kare)

text = "hello world"
print(text.endswith("world"))   # True

# 1️⃣3️⃣ isdigit() → Check karta hai string sirf numbers hai ya nahi

text = "12345"
print(text.isdigit())   # True

# 1️⃣4️⃣ isalpha() → Check karta hai string sirf alphabets hai ya nahi

text = "Python"
print(text.isalpha())   # True

# 1️⃣5️⃣ isalnum() → Alphabet + numbers allowed (space nahi)

text = "Python123"
print(text.isalnum())   # True

# ⭐ Bonus — String Slicing (Bahut Important)

text = "PYTHON"
print(text[0:3])   # PYT
print(text[:4])    # PYTH
print(text[-3:])   # HON

```

# 📝 Python List

Python me List ek ordered, mutable (changeable) collection hoti hai, jisme multiple items (different data types) store kiye ja sakte hain.

`my_list = [10, "Hello", 3.5, True]`


```python
# 1️⃣ append() → List ke end me item add karta hai

nums = [1, 2, 3]
nums.append(4)
print(nums)   # [1, 2, 3, 4]

# 2️⃣ insert(index, value) → Specific position par value insert

nums = [10, 20, 30]
nums.insert(1, 15)
print(nums)   # [10, 15, 20, 30]

# 3️⃣ extend() → Ek list ke saath dusri list merge

a = [1, 2]
b = [3, 4]
a.extend(b)
print(a)   # [1, 2, 3, 4]

# 4️⃣ remove() → Value ko remove karta hai

nums = [1, 2, 3, 2]
nums.remove(2)
print(nums)   # [1, 3, 2]   (sirf first 2 remove hota hai)

# 5️⃣ pop() → Index ke base par element remove + return

nums = [10, 20, 30]
nums.pop(1)
print(nums)   # [10, 30]

# 6️⃣ clear() → Puri list empty

nums = [1, 2, 3]
nums.clear()
print(nums)   # []

# 7️⃣ index() → Value ka index return karta hai

nums = [5, 10, 15]
print(nums.index(10))   # 1

# 8️⃣ count() → Value kitni baar aayi hai

nums = [1, 2, 2, 3]
print(nums.count(2))   # 2

# 9️⃣ sort() → List ko ascending order me sort karta hai

nums = [4, 1, 3, 2]
nums.sort()
print(nums)   # [1, 2, 3, 4]

# 🔟 reverse() → List ko ulta kar deta hai

nums = [1, 2, 3]
nums.reverse()
print(nums)   # [3, 2, 1]

# ⭐ Bonus Concept — List Slicing (Bahut Important)

nums = [10, 20, 30, 40, 50]
print(nums[1:4])   # [20, 30, 40]
print(nums[:3])    # [10, 20, 30]
print(nums[-2:])   # [40, 50]

# ⭐ List Loop (Iteration)

nums = [10, 20, 30]
for n in nums:
    print(n)
```

# 📝 Python Tuple

Python me Tuple ek ordered, immutable (change-na-hone-wala) collection hota hai.
    
List jaisa hota hai, lekin tuple ko modify nahi kar sakte.

`my_tuple = (10, 20, 30, 40)`

* ✔ Indexing supported
* ✔ Duplicate values allowed
* ❌ Change / Add / Remove not allowed


```python
# 1️⃣ count() → Value kitni baar aayi hai

t = (1, 2, 2, 3)
print(t.count(2))   # 2

# 2️⃣ index() → Value ka index return

t = (10, 20, 30)
print(t.index(20))   # 1

# ⭐ Bonus — Tuple Slicing (List jaisa)

t = (10, 20, 30, 40, 50)
print(t[1:4])  # (20, 30, 40)
print(t[:3])   # (10, 20, 30)
print(t[-2:])  # (40, 50)


### 🔥 Tuple Packing & Unpacking (Bahut Important)
# 🎁 Packing

t = 10, 20, 30
print(t)   # (10, 20, 30)

# 📦 Unpacking

a, b, c = (10, 20, 30)
print(a, b, c)   # 10 20 30

# Single Element Tuple Important Note

t = (10,)   # Single element tuple
print(type(t))   # <class 'tuple'>
```


```python
# 1️⃣ How to Add Value in Tuple

### Tuple immutable hota hai, isliye direct add nahi kar sakte.
### But list me convert karke add kar sakte hain → phir tuple me convert.

t = (10, 20, 30)
temp = list(t)
temp.append(40)
t = tuple(temp)
print(t)   # (10, 20, 30, 40)

# 2️⃣ Tuple Slicing ===>  List jaisa hi slicing hota hai.

t = (10, 20, 30, 40, 50)
print(t[1:4])   # (20, 30, 40)
print(t[:3])    # (10, 20, 30)
print(t[-2:])   # (40, 50)

# 3️⃣ Value Get (Indexing) ===>  Specific position ki value lene ke liye index use.

t = (5, 10, 15, 20)
print(t[2])   # 15
print(t[-1])  # 20

# 4️⃣ Concatenation (2 Tuples Ko Jodna)   ===>>>  + operator se 2 tuples ko combine kar sakte hain.

t1 = (1, 2, 3)
t2 = (4, 5)
t3 = t1 + t2
print(t3)   # (1, 2, 3, 4, 5)

# 5️⃣ Remove Value from Tuple

# Direct remove nahi hota, kyunki tuple immutable hai.
# But list ke through trick se remove kar sakte hain:

t = (10, 20, 30, 20)
temp = list(t)
temp.remove(20)  # first 20 remove
t = tuple(temp)
print(t)   # (10, 30, 20)

# 6️⃣ del — Tuple Delete ===>> del se poora tuple delete ho jata hai, element delete nahi hota.

t = (10, 20, 30)
del t
print(t)   # ❌ Error — tuple does not exist

# 7️⃣ join() — Important Clarification

# 👉 join() tuple ka method nahi hota
# join actually string method hota hai jo tuple ke strings ko join karta hai.

t = ("A", "B", "C")
result = "-".join(t)
print(result)   # A-B-C
```

# ⭐ Difference Between List and Tuple (Quick Revision)

| Feature  | List                  | Tuple                   |
| -------- | --------------------- | ----------------------- |
| Syntax   | `[ ]`                 | `( )`                   |
| Mutable  | Yes                   | No                      |
| Speed    | Slow                  | Fast                    |
| Methods  | More                  | Very few                |
| Use Case | Data change hota rahe | Data fixed hona chahiye |


# 📝 Python Set

Python me Set ek unordered, unindexed, mutable collection hota hai jisme duplicate values allowed nahi hoti.

`my_set = {10, 20, 30, 40}`


```python
# 1️⃣ add() — Set me new value add karna

s = {1, 2, 3}
s.add(4)
print(s)   # {1, 2, 3, 4}

# 2️⃣ update() — Multiple values add / merge

s = {1, 2}
s.update([3, 4, 5])
print(s)   # {1, 2, 3, 4, 5}

# 3️⃣ remove() — Value remove but nahi mili to error

s = {10, 20, 30}
s.remove(20)
print(s)   # {10, 30}

# 4️⃣ discard() — Value remove karta par error nahi deta

s = {10, 20, 30}
s.discard(40)
print(s)   # {10, 20, 30}

# 5️⃣ pop() — Random element remove + return

s = {1, 2, 3}
item = s.pop()
print(item)  # Random element
print(s)

# 6️⃣ clear() — Set empty

s = {1, 2, 3}
s.clear()
print(s)   # set()

# ✔ union() → Sare unique values (OR operation)

a = {1, 2, 3}
b = {3, 4, 5}
print(a.union(b))   # {1, 2, 3, 4, 5}

# ✔ intersection() → Common values (AND operation)

a = {1, 2, 3}
b = {2, 3, 4}
print(a.intersection(b))   # {2, 3}

# ✔ difference() → a me jo hain but b me nahi

a = {1, 2, 3}
b = {2, 3}
print(a.difference(b))   # {1}

# ✔ symmetric_difference() → Unique in both (XOR)

a = {1, 2, 3}
b = {3, 4}
print(a.symmetric_difference(b))   # {1, 2, 4}

# 🎁 Check Membership — in keyword

s = {10, 20, 30}
print(20 in s)   # True
print(50 in s)   # False
```

# 📝 Python Dictionary

Python me Dictionary ek unordered, mutable collection hota hai jo key–value pairs ke form me data store karta hai.

`student = {"name": "Rahul", "age": 20, "city": "Delhi"}`


```python
# 1️⃣ get() → Key ki value safely return karta hai

d = {"name": "Aman", "age": 22}
print(d.get("age"))         # 22
print(d.get("city"))        # None (Error nahi deta)

# 2️⃣ keys() → Saare keys return

d = {"a": 1, "b": 2}
print(d.keys())    # dict_keys(['a', 'b'])

# 3️⃣ values() → Saari values return

d = {"a": 1, "b": 2}
print(d.values())   # dict_values([1, 2])

# 4️⃣ items() → Key + Value pair return

d = {"a": 1, "b": 2}
print(d.items())    # dict_items([('a', 1), ('b', 2)])

# 5️⃣ update() → Dictionary me value update / add

d = {"a": 1, "b": 2}
d.update({"b": 20, "c": 30})
print(d)    # {'a': 1, 'b': 20, 'c': 30}

# 6️⃣ pop() → Specific key remove + value return

d = {"a": 1, "b": 2, "c": 3}
d.pop("b")
print(d)    # {'a': 1, 'c': 3}

# 7️⃣ popitem() → Last inserted key–value hatata + return

d = {"a": 1, "b": 2, "c": 3}
d.popitem()
print(d)    # {'a': 1, 'b': 2}

# 8️⃣ clear() → Puri dictionary empty

d = {"x": 10, "y": 20}
d.clear()
print(d)   # {}

# 9️⃣ fromkeys() → Keys ke base par dict create

keys = ["a", "b", "c"]
d = dict.fromkeys(keys, 0)
print(d)   # {'a': 0, 'b': 0, 'c': 0}

#🔥 Dictionary — Add / Update / Remove Shortcut

#✔ Add

d = {"x": 1}
d["y"] = 2
print(d)   # {'x': 1, 'y': 2}

# ✔ Update value

d["x"] = 100
print(d)   # {'x': 100, 'y': 2}

# ✔ Delete key

del d["y"]
print(d)   # {'x': 100}

# ⭐ Loop Dictionary

d = {"name": "Rohan", "age": 21}

for key in d:
    print(key, d[key])
```

    22
    None
    dict_keys(['a', 'b'])
    dict_values([1, 2])
    dict_items([('a', 1), ('b', 2)])
    {'a': 1, 'b': 20, 'c': 30}
    {'a': 1, 'c': 3}
    {'a': 1, 'b': 2}
    {}
    {'a': 0, 'b': 0, 'c': 0}
    {'x': 1, 'y': 2}
    {'x': 100, 'y': 2}
    {'x': 100}
    name Rohan
    age 21
    

# Argument vs Parameter Python

## 🔷 Parameter (Function Definition ke Time)

📌 Parameter wo variable hote hain **jo function define karte waqt likhe jaate hain**. 

Ye input receive karne ke placeholder hote hain.

🔹 Parameter = Function ke andar data receive karne ke liye naam

### Example
```python
def add(a, b):   # a and b = parameters
    return a + b
```
## 🔷 Argument (Function Call ke Time)

📌 Argument wo real values hoti hain jo function ko call karte waqt pass ki jati hain.

```python
result = add(5, 10)   # 5 and 10 = arguments


| Feature          | Parameter                  | Argument                 |
| ---------------- | -------------------------- | ------------------------ |
| Kab use hota hai | Function define karte waqt | Function call karte waqt |
| Kya hota hai     | Variable name              | Actual value             |
| Position         | Function header            | Function calling         |
| Example          | `a, b`                     | `5, 10`                  |


`Parameter` = Function ke andar input receive karne ka placeholder,

`Argument` = Function ko call karte waqt diya gaya actual data

```

# 🔥 async & await Python

Python me jab hame asynchronous programming karni hoti hai (yaani code parallel tarike se chalana without blocking the program), tab async & await use hota hai.

Normally Python code step by step chalta hai:

`Step 1 → Step 2 → Step 3 ...`

Lekin asynchronous code me multiple tasks ek sath chal sakte hain, jisse program fast ho jata hai — specially jab network request, database call, file download jaisi slow operations ho.

## 📌 async ka matlab

async ka use function ko asynchronous function banane ke liye hota hai.

```py
`async def my_function():
    ...
```

## 📌 await ka matlab

await ka use async function ke andar hota hai, jab hum kisi asynchronous task ke complete hone ka wait karte hain — bina pura program ko block kiye.

```py
    await some_async_task()
```


```python
## Example

import asyncio

async def download_file():
    print("Download started...")
    await asyncio.sleep(3)   # ye 3 seconds wait karega but program block nahi hoga
    print("Download complete!")

async def main():
    await download_file()

asyncio.run(main())

```


```python
# Example

import asyncio

async def task1():
    print("Task 1 started")
    await asyncio.sleep(3)
    print("Task 1 done")

async def task2():
    print("Task 2 started")
    await asyncio.sleep(2)
    print("Task 2 done")

async def main():
    await asyncio.gather(task1(), task2())

asyncio.run(main())

```


```python
#Output
Task 1 started
Task 2 started
(wait 2 sec)
Task 2 done
(wait 1 sec)
Task 1 done
```

# 🔥 Asynchronous Programming


### Normal programming (Synchronous)

Jab program ek line complete hone ke baad hi next line chalata hai.
`Task 1 → Task 2 → Task 3`

Agar Task 1 slow hai (jaise network request / database / file download), to purā program ruk jata hai us task ke complete hone ka wait karte hue.


### Asynchronous programming

Isme program slow task ke complete hone ka wait nahi karta, balki jab tak wo slow task complete ho, tab tak baaki tasks parallel me chalte rehte hain.

```python
Task 1 (slow) ────────────▶
Task 2 ──▶
Task 3 ──▶
```


```python
### 🧠 Simple Python Example Compare

##### ❌ Synchronous (Slow)

download_file()  # 5 sec
send_email()     # 3 sec
log_report()     # 2 sec

Total time = 5 + 3 + 2 = 10 sec

##### ✔ Asynchronous (Fast)

download_file() 5 sec
send_email()    3 sec
log_report()    2 sec


Teeno same time pe start hote hain
Total time = max(5, 3, 2) = 5 sec only
```

# UseCase

| Task Type                   | Best Approach                                 |
| --------------------------- | --------------------------------------------- |
| Network request (API calls) | Async                                         |
| Database queries            | Async                                         |
| Emails sending              | Async                                         |
| Files download/uploads      | Async                                         |
| Heavy CPU calculations      | Async nahi — multiprocessing/threading better |



# Match Case in Python

## Match Case Kya Hota Hai?

`match-case` Python ka ek **pattern matching statement** hai jo Python 3.10 me introduce hua tha.

Ye bahut had tak dusri programming languages ke **switch-case** statement jaisa kaam karta hai.

Iska use multiple conditions ko clean aur readable way me handle karne ke liye kiya jata hai.

---

## Syntax

```python
match variable:
    case value1:
        # code
    case value2:
        # code
    case _:
        # default code
```

---

## Simple Example

```python
day = 2

match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Invalid Day")
```

### Output

```text
Tuesday
```

---

## case _ Kya Hota Hai?

`_` default case hota hai.

Agar koi bhi condition match nahi hoti to ye execute hota hai.

```python
number = 10

match number:
    case 1:
        print("One")
    case 2:
        print("Two")
    case _:
        print("Unknown Number")
```

### Output

```text
Unknown Number
```

---

## Multiple Values Match Karna

```python
status = 400

match status:
    case 200:
        print("Success")
    case 400 | 401 | 403:
        print("Client Error")
    case 500:
        print("Server Error")
```

### Output

```text
Client Error
```

---

## Match Case vs If-Else

### Using If-Else

```python
day = 2

if day == 1:
    print("Monday")
elif day == 2:
    print("Tuesday")
elif day == 3:
    print("Wednesday")
else:
    print("Invalid Day")
```

### Using Match Case

```python
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Invalid Day")
```

`match-case` code ko jyada readable aur clean bana deta hai jab bahut saari conditions ho.

---

## Advantages

- Code readable hota hai.
- Multiple conditions easily handle hoti hain.
- Switch-case jaisa syntax milta hai.
- Complex pattern matching support karta hai.

---

## Important Points

- Python 3.10+ me available hai.
- `switch-case` ka alternative mana jata hai.
- Default case ke liye `_` use kiya jata hai.
- Pattern matching support karta hai.

---

## Interview Answer (Short)

**Match-case Python 3.10 me introduce hua ek pattern matching statement hai jo switch-case ki tarah kaam karta hai. Iska use multiple conditions ko clean aur readable way me handle karne ke liye kiya jata hai. Default case ke liye `_` use hota hai.**

# File Handling in Python

File Handling ek process hai jiske through Python program files ke saath interact karta hai.

Iski help se hum file me stored data ko access, manage aur modify kar sakte hain. File system me maujood data ko program ke andar use karne ke liye file handling ka use kiya jata hai.

---

## Writing Data into a File

```python
file = open("student.txt", "w")

file.write("My name is Bittu")
file.close()
```

### Explanation

- `open()` file ko open karta hai.
- `"w"` mode file me data write karne ke liye use hota hai.
- `write()` file me data save karta hai.
- `close()` file ko close karta hai.

---

## Reading Data from a File

```python
file = open("student.txt", "r")

data = file.read()
print(data)

file.close()
```

### Explanation

- `"r"` mode file ko read karne ke liye use hota hai.
- `read()` file ka pura content read karta hai.
- `print()` content ko screen par display karta hai.
- `close()` file ko close karta hai.

---

# Difference Between readline() and writelines() in Python

## readline()

`readline()` ka use file se **ek time par sirf ek line** read karne ke liye kiya jata hai.

### Example

File Content (`student.txt`)

```text
Bittu
Rahul
Aman
```

```python
file = open("student.txt", "r")

line1 = file.readline()
line2 = file.readline()

print(line1)
print(line2)

file.close()
```

### Output

```text
Bittu

Rahul
```

### Explanation

- Pehli `readline()` first line read karegi.
- Dusri `readline()` second line read karegi.
- Har call next line par move ho jati hai.

---

## writelines()

`writelines()` ka use ek saath multiple lines ko file me write karne ke liye kiya jata hai.

### Example

```python
file = open("student.txt", "w")

data = [
    "Bittu\n",
    "Rahul\n",
    "Aman\n"
]

file.writelines(data)

file.close()
```

### File Content After Execution

```text
Bittu
Rahul
Aman
```

### Explanation

- `writelines()` list ya iterable ko accept karta hai.
- List ke saare elements file me write ho jate hain.
- `writelines()` automatically new line (`\n`) add nahi karta, hume khud dena padta hai.

---

## readline() vs writelines()

| readline() | writelines() |
|------------|-------------|
| File se data read karta hai | File me data write karta hai |
| Ek baar me ek line read karta hai | Ek baar me multiple lines write karta hai |
| Read operation hai | Write operation hai |
| Mostly `"r"` mode ke saath use hota hai | Mostly `"w"` ya `"a"` mode ke saath use hota hai |

---

## Interview Answer (Short)

**`readline()` file se ek time par ek line read karne ke liye use hota hai, jabki `writelines()` multiple lines ko ek saath file me write karne ke liye use hota hai. `writelines()` automatic newline add nahi karta, isliye `\n` manually dena padta hai.**


# tell(), seek() and truncate() in Python

## tell()

`tell()` current file cursor (pointer) ki position batata hai.

### Example

```python
file = open("student.txt", "r")

print(file.tell())

file.read(5)

print(file.tell())

file.close()
```

### Output

```text
0
5
```

### Explanation

- Starting me cursor position `0` hoti hai.
- 5 characters read karne ke baad cursor position `5` ho jati hai.

---

## seek()

`seek()` cursor ko kisi specific position par le jane ke liye use hota hai.

### Example

```python
file = open("student.txt", "r")

file.seek(3)

print(file.read())

file.close()
```

### File Content

```text
Bittu
```

### Output

```text
tu
```

### Explanation

- `seek(3)` cursor ko 3rd index par le gaya.
- Read wahin se start hua.

---

## truncate()

`truncate()` file ke content ko specified size tak cut kar deta hai.

### Example

```python
file = open("student.txt", "r+")

file.truncate(5)

file.close()
```

### Before

```text
Bittu Kumar
```

### After

```text
Bittu
```

### Explanation

- `truncate(5)` sirf pehle 5 characters rakhega.
- Baaki content remove ho jayega.

---

## Interview Answer (Short)

- **tell()** → Current cursor position batata hai.
- **seek()** → Cursor ko specific position par le jata hai.
- **truncate()** → File ke content ko specified size tak cut kar deta hai.