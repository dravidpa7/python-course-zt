# Python Beginner's Guide

---

## MODULE 1: Basic Fundamentals of Python

### 1. Print("Hello World")
**What it does:** Displays output (text/values) on the screen.

**How it works:** `print()` is a built-in function. Anything inside the parentheses gets sent to your console/terminal as output.

```python
print("Hello, World!")
# Output: Hello, World!
```

---

### 2. Variables
**What it does:** A variable is a named container that stores a value in memory so you can reuse or change it later.

**How it works:** Python figures out the data type automatically (no need to declare `int`, `str`, etc. like in C/Java). You just assign with `=`.

```python
name = "Dravid"
age = 21
is_developer = True

print(name, age, is_developer)
# Output: Dravid 21 True
```

---

### 3. Stack & Heap Memory
**What it does:** Explains *where* Python actually stores your variables and data while a program runs.

**How it works:**
- **Stack memory** stores function calls and simple references (the variable *name* and a pointer to where its value lives). It's fast, and cleared automatically when a function finishes.
- **Heap memory** stores the actual objects (lists, strings, custom objects, etc.). It's slower but flexible, and managed by Python's garbage collector.

When you write `x = [1, 2, 3]`, the name `x` lives on the stack, but the actual list `[1, 2, 3]` lives on the heap. `x` just "points" to it.

```python
x = [1, 2, 3]   # x (stack) points to the list object (heap)
y = x           # y points to the SAME heap object as x
y.append(4)

print(x)  # [1, 2, 3, 4]  <- x changed too, because they share the same heap object!
```

---

### 4. `id()` Function
**What it does:** Returns the unique memory address (identity) of an object — proof of the stack/heap concept above.

**How it works:** Every object in Python has a unique ID for its lifetime. Two variables pointing to the same object will share the same `id()`.

```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(id(a) == id(b))  # True  -> same object in memory
print(id(a) == id(c))  # False -> different object, even though values look equal
```

---

### 5. Python Comments
**What it does:** Lets you write notes in your code that Python ignores when running — used for explanations, not execution.

**How it works:** `#` starts a single-line comment. Triple quotes `''' '''` or `""" """` are used for multi-line comments/docstrings.

```python
# This is a single-line comment
print("Hello")  # This runs, comment is ignored

"""
This is a
multi-line comment
"""
```

---

### 6. Data Types in Python
**What it does:** Defines the *kind* of value a variable holds — this decides what operations you can do with it.

**How it works:** Python has built-in types like:
- `int` (whole numbers)
- `float` (decimals)
- `str` (text)
- `bool` (True/False)
- `list`, `tuple`, `dict`, `set` (collections)

Use `type()` to check a variable's type.

```python
num = 10          # int
price = 99.99      # float
name = "Dravid"     # str
is_active = True    # bool

print(type(num))    # <class 'int'>
print(type(price))  # <class 'float'>
```

---

### 7. Input Function in Python
**What it does:** Takes input from the user while the program is running.

**How it works:** `input()` always returns a **string**, even if the user types a number — you must manually convert it if you need a number.

```python
name = input("What's your name? ")
age = int(input("What's your age? "))  # convert string -> int

print(f"Hi {name}, you are {age} years old.")
```

---

## MODULE 2: Print Function (Deep Dive)

**What it does:** Beyond basic printing, `print()` has parameters that control formatting: `sep`, `end`, and multiple ways to insert variables into text.

**How it works:**
- `sep` controls what goes *between* multiple items (default is a space).
- `end` controls what goes *after* the print statement (default is a newline).
- f-strings (`f"..."`) let you embed variables directly inside text.

```python
print("Python", "is", "fun", sep="-")     # Python-is-fun
print("Hello", end=" ")
print("World")                             # Hello World (same line)

name = "Dravid"
print(f"Welcome, {name}!")                 # Welcome, Dravid!
```

---

## MODULE 3: Operators in Python

**What it does:** Operators perform actions on values — math, comparisons, logic, and assignment.

**How it works:**
- **Arithmetic:** `+ - * / // % **`
- **Comparison:** `== != > < >= <=` (returns True/False)
- **Logical:** `and or not`
- **Assignment:** `= += -= *= /=`

```python
a, b = 10, 3

print(a + b)   # 13
print(a // b)  # 3   (floor division, drops decimal)
print(a % b)   # 1   (remainder)
print(a ** b)  # 1000 (power)

print(a > b and b > 0)  # True (logical AND)
```

---

## MODULE 4: Control Flow

**What it does:** Lets your program make decisions and run different code depending on a condition.

**How it works:** `if`, `elif`, `else` check conditions top to bottom, and run the block under the **first** one that's True.

```python
marks = 75

if marks >= 90:
    print("Grade A")
elif marks >= 60:
    print("Grade B")
else:
    print("Grade C")

# Output: Grade B
```

---

## MODULE 5: Loops in Python

**What it does:** Repeats a block of code multiple times without rewriting it.

**How it works:**
- `for` loop: iterates over a known sequence (list, range, string).
- `while` loop: repeats as long as a condition stays True.
- `break` exits a loop early, `continue` skips to the next iteration.

```python
# for loop
for i in range(5):
    print(i)   # 0 1 2 3 4

# while loop
count = 0
while count < 3:
    print("Counting:", count)
    count += 1

# break/continue
for i in range(10):
    if i == 3:
        continue   # skip 3
    if i == 6:
        break      # stop at 6
    print(i)       # 0 1 2 4 5
```

---

## MODULE 6: Strings in Python

**What it does:** Strings represent text, and Python has built-in tools to slice, search, and manipulate them.

**How it works:** Strings are **immutable** (can't be changed in place) and support indexing/slicing like lists.

```python
text = "Python Programming"

print(text[0])          # 'P' (indexing)
print(text[0:6])        # 'Python' (slicing)
print(text.lower())     # 'python programming'
print(text.upper())     # 'PYTHON PROGRAMMING'
print(text.replace("Python", "Java"))  # 'Java Programming'
print(text.split(" "))  # ['Python', 'Programming']
print(len(text))        # 19
```

---

## MODULE 7: Lists

**What it does:** A list stores an ordered, changeable collection of items (can hold mixed data types).

**How it works:** Lists are **mutable** — you can add, remove, or update items after creation. Indexed starting at 0.

```python
fruits = ["apple", "banana", "cherry"]

fruits.append("mango")     # add to end
fruits.remove("banana")    # remove by value
fruits[0] = "grape"        # update by index

print(fruits)          # ['grape', 'cherry', 'mango']
print(fruits[-1])      # 'mango' (last item)
print(len(fruits))     # 3
```

---

## MODULE 8: Tuples

**What it does:** A tuple is like a list, but **immutable** — once created, its values can't be changed. Used for fixed data.

**How it works:** Defined with `()` instead of `[]`. Faster than lists and often used for things that shouldn't change, like coordinates.

```python
coordinates = (10, 20)
print(coordinates[0])   # 10

# coordinates[0] = 99   # This would raise an ERROR - tuples can't be modified

x, y = coordinates      # unpacking
print(x, y)             # 10 20
```

---

## MODULE 9: Dictionary

**What it does:** Stores data as **key-value pairs**, letting you look up a value by a unique key instead of a numeric index.

**How it works:** Defined with `{}`. Keys must be unique; values can be anything.

```python
student = {
    "name": "Dravid",
    "age": 21,
    "course": "CS"
}

print(student["name"])       # Dravid
student["age"] = 22          # update value
student["grade"] = "A"       # add new key

for key, value in student.items():
    print(key, "->", value)
```

---

## MODULE 10: Sets

**What it does:** Stores an **unordered collection of unique items** — automatically removes duplicates.

**How it works:** Defined with `{}` (like a dict but no key:value pairs). Great for removing duplicates or checking membership fast.

```python
numbers = {1, 2, 2, 3, 3, 3, 4}
print(numbers)   # {1, 2, 3, 4}  <- duplicates auto-removed

numbers.add(5)
print(5 in numbers)   # True (fast membership check)

a = {1, 2, 3}
b = {2, 3, 4}
print(a & b)   # {2, 3} -> intersection
print(a | b)   # {1, 2, 3, 4} -> union
```

---

## MODULE 11: Functions

### 1. Functions Introduction
**What it does:** A function is a reusable block of code that performs a specific task, so you don't repeat yourself.

**How it works:** Define once with `def`, call it as many times as you want.

```python
def greet():
    print("Hello!")

greet()  # call it
greet()  # call again
```

---

### 2. Defining a Function
**What it does:** The `def` keyword creates a function's structure — its name, parameters, and body.

**How it works:** Syntax: `def function_name(parameters):` followed by an indented block.

```python
def add(a, b):
    result = a + b
    print(result)

add(5, 3)   # 8
```

---

### 3. Docstrings
**What it does:** A special string right after the function definition that documents what the function does.

**How it works:** Written with triple quotes; accessible via `function.__doc__` or `help()`.

```python
def add(a, b):
    """Returns the sum of two numbers."""
    return a + b

print(add.__doc__)   # Returns the sum of two numbers.
```

---

### 4. Parameters & Arguments
**What it does:** Parameters are placeholders in the function definition; arguments are the actual values you pass in when calling it.

**How it works:** `def greet(name):` — `name` is a **parameter**. `greet("Dravid")` — `"Dravid"` is the **argument**.

```python
def greet(name):     # name = parameter
    print(f"Hello, {name}")

greet("Dravid")       # "Dravid" = argument
```

---

### 5. Return
**What it does:** Sends a value back from the function to wherever it was called, so you can use/store the result.

**How it works:** `return` stops the function and hands the value back. Without `return`, a function gives back `None`.

```python
def square(n):
    return n * n

result = square(4)
print(result)   # 16
```

---

### 6. Returning Multiple Values
**What it does:** A single function can return more than one value at once, packed as a tuple.

**How it works:** Separate the return values with commas — Python auto-packs them into a tuple, which you can unpack on the calling side.

```python
def get_min_max(numbers):
    return min(numbers), max(numbers)

low, high = get_min_max([4, 2, 9, 1])
print(low, high)   # 1 9
```

---

### 7. Scope of a Variable
**What it does:** Determines *where* in your code a variable can be accessed — inside a function only, or everywhere.

**How it works:**
- **Local scope:** variables created inside a function only exist inside it.
- **Global scope:** variables created outside functions can be read anywhere (use `global` keyword to modify them inside a function).

```python
x = 10   # global variable

def show():
    y = 5   # local variable
    print(x, y)   # can read global x here

show()          # 10 5
print(x)        # 10
# print(y)      # ERROR - y doesn't exist outside the function
```

---

### 8. Lambda Function
**What it does:** A short, one-line anonymous function — used when you need a quick function without formally defining one with `def`.

**How it works:** Syntax: `lambda arguments: expression`. Commonly used with `map()`, `filter()`, `sorted()`.

```python
square = lambda n: n * n
print(square(5))   # 25

nums = [1, 2, 3, 4]
doubled = list(map(lambda x: x * 2, nums))
print(doubled)   # [2, 4, 6, 8]
```

---

### 9. Challenge: Print Even Numbers
**What it does:** Practice combining loops + conditionals to filter numbers.

```python
def print_even(numbers):
    for n in numbers:
        if n % 2 == 0:
            print(n)

print_even([1, 2, 3, 4, 5, 6])   # 2 4 6
```

---

### 10. Challenge: Return List with Unique Numbers
**What it does:** Practice combining functions + sets to remove duplicates.

```python
def unique_numbers(numbers):
    return list(set(numbers))

print(unique_numbers([1, 2, 2, 3, 3, 4]))   # [1, 2, 3, 4]
```

---

### 11. Arguments vs Parameters (Recap)
**What it does:** Clarifies the terminology so it stops being confusing.

**How it works:** Parameter = the variable name in the function definition. Argument = the actual value sent when calling.

```python
def multiply(x, y):     # x, y = parameters
    return x * y

print(multiply(3, 4))    # 3, 4 = arguments -> 12
```

---

### 12. Positional Arguments
**What it does:** Arguments matched to parameters based on their **order** (position), not name.

**How it works:** The first argument fills the first parameter, second fills second, and so on.

```python
def describe(name, age):
    print(f"{name} is {age} years old")

describe("Dravid", 21)   # name="Dravid", age=21 (matched by position)
```

---

### 13. Default Arguments
**What it does:** Lets a parameter have a fallback value if the caller doesn't provide one.

**How it works:** Set the default with `=` in the function definition.

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Dravid")               # Hello, Dravid!
greet("Dravid", "Welcome")     # Welcome, Dravid!
```

---

### 14. Default Follows Non-Default
**What it does:** A Python rule — parameters *with* defaults must come **after** parameters *without* defaults.

**How it works:** This is invalid: `def greet(greeting="Hi", name):` — Python won't know how to fill `name` unambiguously. The correct order is required-first, defaults-last.

```python
# CORRECT
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}")

# WRONG - this raises a SyntaxError
# def greet(greeting="Hello", name):
#     print(f"{greeting}, {name}")
```

---

### 15. Arbitrary Arguments (`*args`)
**What it does:** Lets a function accept **any number** of positional arguments, when you don't know in advance how many will be passed.

**How it works:** `*args` collects extra positional arguments into a tuple.

```python
def add_all(*args):
    return sum(args)

print(add_all(1, 2, 3))         # 6
print(add_all(1, 2, 3, 4, 5))   # 15
```

---

### 16. Keyword Arguments (`**kwargs`)
**What it does:** Lets you pass arguments by explicitly naming the parameter, in any order — and `**kwargs` collects any number of extra named arguments into a dictionary.

**How it works:** `key=value` syntax when calling; `**kwargs` in the function definition gathers them.

```python
def describe(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

describe(name="Dravid", age=21, course="CS")
# name: Dravid
# age: 21
# course: CS
```

---

## Quick Reference Cheat Sheet

| Concept | One-line takeaway |
|---|---|
| Variables | Named storage, no type declaration needed |
| `id()` | Shows an object's unique memory address |
| Lists | Ordered, mutable, `[]` |
| Tuples | Ordered, immutable, `()` |
| Dictionaries | Key-value pairs, `{}` |
| Sets | Unique unordered items, `{}` |
| `*args` | Any number of positional arguments |
| `**kwargs` | Any number of keyword arguments |
| Lambda | One-line anonymous function |

---

*Tip: Don't just read these — open a Python file and type every example yourself. Typing builds muscle memory faster than reading.*
