# Python Beginner's Guide — Part 2
### Modules 14 – 16 | Format for every topic: **What it does → How it works → Example**

---

## MODULE 14: OOP in Python

### 1. Intro to OOPs in Python
**What it does:** Object-Oriented Programming is a way of organizing code around **objects** — things that bundle data (attributes) and behavior (methods) together, instead of writing everything as loose functions and variables.

**How it works:** Real-world things become blueprints (**classes**) and specific instances (**objects**). E.g., "Car" is a class; "your red Honda" is an object of that class. The 4 pillars of OOP are: **Encapsulation, Inheritance, Polymorphism, and Abstraction.**

```python
# Without OOP - loose, disorganized
car1_brand = "Honda"
car1_speed = 0

# With OOP - organized as a blueprint
class Car:
    pass

car1 = Car()   # an actual object, built from the blueprint
```

---

### 2. Class & Object in Python
**What it does:** A **class** is the blueprint/template. An **object** is a real, usable instance created from that blueprint.

**How it works:** Define a class with `class ClassName:`. Create an object by calling the class like a function: `object = ClassName()`.

```python
class Car:
    def honk(self):
        print("Beep beep!")

my_car = Car()      # my_car is an OBJECT of class Car
my_car.honk()        # Beep beep!

another_car = Car()  # a completely separate object
```

---

### 3. Class Constructor
**What it does:** Automatically runs setup code the moment an object is created — usually to assign initial values to its attributes.

**How it works:** The constructor method is always named `__init__`. It runs automatically when you call `ClassName()`. `self` refers to the object being built.

```python
class Car:
    def __init__(self, brand, speed):
        self.brand = brand     # runs automatically on creation
        self.speed = speed

my_car = Car("Honda", 0)   # __init__ runs here immediately
print(my_car.brand)         # Honda
```

---

### 4. Class Methods
**What it does:** Functions defined inside a class that describe what objects of that class can *do* — their behavior.

**How it works:** Defined like normal functions but indented inside the class, and always take `self` as the first parameter so they can access that specific object's data.

```python
class Car:
    def __init__(self, brand, speed):
        self.brand = brand
        self.speed = speed

    def accelerate(self):          # a method
        self.speed += 10
        print(f"{self.brand} is now going {self.speed} km/h")

my_car = Car("Honda", 0)
my_car.accelerate()   # Honda is now going 10 km/h
my_car.accelerate()   # Honda is now going 20 km/h
```

---

### 5. Class Variables
**What it does:** A variable **shared by all objects** of a class, instead of being unique to each object (unlike `self.x` attributes).

**How it works:** Defined directly inside the class body, outside any method. All instances see the same value unless explicitly overridden on a specific object.

```python
class Car:
    wheels = 4   # class variable - same for every car

    def __init__(self, brand):
        self.brand = brand   # instance variable - unique per object

car1 = Car("Honda")
car2 = Car("Toyota")

print(car1.wheels, car2.wheels)   # 4 4  (shared)
Car.wheels = 6                     # change for ALL cars
print(car1.wheels, car2.wheels)   # 6 6
```

---

### 6. Adding More Methods in Class
**What it does:** Shows that a class can hold as many methods as needed to fully describe an object's behavior.

**How it works:** Just keep adding indented `def` blocks inside the class — each becomes a callable action for any object of that class.

```python
class Car:
    def __init__(self, brand, speed=0):
        self.brand = brand
        self.speed = speed

    def accelerate(self):
        self.speed += 10

    def brake(self):
        self.speed = max(0, self.speed - 10)

    def display_speed(self):
        print(f"{self.brand}'s speed: {self.speed} km/h")

my_car = Car("Honda")
my_car.accelerate()
my_car.accelerate()
my_car.brake()
my_car.display_speed()   # Honda's speed: 10 km/h
```

---

### 7. Inheritance Introduction
**What it does:** Lets a new class reuse the attributes and methods of an existing class, instead of rewriting them from scratch.

**How it works:** The class being reused is the **parent/base class**. The new class is the **child/derived class**, created by passing the parent's name in parentheses.

```python
class Vehicle:              # parent class
    def start_engine(self):
        print("Engine started")

class Car(Vehicle):          # child class - inherits from Vehicle
    pass

my_car = Car()
my_car.start_engine()   # Engine started (inherited, not rewritten)
```

---

### 8. Inheritance Code
**What it does:** Shows a fuller working example of a child class using everything it inherited from its parent.

**How it works:** The child automatically gets every method and attribute the parent has — you don't have to redeclare anything unless you want to change it.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} is eating")

class Dog(Animal):     # Dog inherits __init__ and eat() from Animal
    pass

d = Dog("Rex")
d.eat()   # Rex is eating (uses Animal's method automatically)
```

---

### 9. Adding Attributes in Derived Class
**What it does:** Lets a child class have its *own* extra attributes on top of what it inherited from the parent.

**How it works:** Define your own `__init__` in the child, call `super().__init__()` to still run the parent's setup, then add the new attribute.

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)   # run parent's __init__ first
        self.breed = breed        # new attribute, only Dog has this

d = Dog("Rex", "Labrador")
print(d.name, d.breed)   # Rex Labrador
```

---

### 10. Adding Methods in Derived Class
**What it does:** Lets a child class have its *own* extra behavior, or override/replace the parent's behavior entirely.

**How it works:** Define a method with the same name as the parent's to **override** it, or a new name to **add** brand-new behavior.

```python
class Animal:
    def speak(self):
        print("Some generic animal sound")

class Dog(Animal):
    def speak(self):              # OVERRIDES parent's speak()
        print("Woof!")

    def fetch(self):               # NEW method, only Dog has this
        print("Fetching the ball!")

d = Dog()
d.speak()    # Woof! (overridden)
d.fetch()    # Fetching the ball! (new, Animal doesn't have this)
```

---

### 11. Polymorphism in Python
**What it does:** "Poly" (many) + "morph" (forms) — the same method name behaves differently depending on which object calls it.

**How it works:** Different classes each define their own version of a method with the identical name; Python automatically calls the right version based on the object's actual class.

```python
class Cat:
    def speak(self):
        print("Meow")

class Dog:
    def speak(self):
        print("Woof")

for animal in [Cat(), Dog()]:
    animal.speak()   # Meow, then Woof - same .speak() call, different result
```

---

### 12. Operator Level Polymorphism
**What it does:** Lets the same operator (like `+`) behave differently depending on the data types involved.

**How it works:** This already happens naturally with built-in types (`+` adds numbers but concatenates strings). You can define this for your own classes too, using dunder methods like `__add__`.

```python
print(3 + 5)         # 8            -> + means "add" for numbers
print("Py" + "thon")  # "Python"     -> + means "join" for strings

class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __add__(self, other):        # redefine + for Point objects
        return Point(self.x + other.x, self.y + other.y)

p1, p2 = Point(1, 2), Point(3, 4)
result = p1 + p2                      # calls __add__ automatically
print(result.x, result.y)             # 4 6
```

---

### 13. Function Level Polymorphism
**What it does:** The same built-in function behaves differently depending on what type of object you pass into it.

**How it works:** Functions like `len()` work on many different types — Python calls the appropriate internal logic for whatever type it receives, without you needing separate function names for each type.

```python
print(len("Python"))        # 6   -> counts characters
print(len([1, 2, 3, 4]))     # 4   -> counts list items
print(len({"a": 1, "b": 2})) # 2   -> counts dictionary keys

# Same function, len(), adapts its behavior based on the input type
```

---

## MODULE 15: File Handling in Python

### 1. Intro to File-Handling in Python
**What it does:** Lets your program save data permanently to disk (files), and load it back later — instead of losing everything when the program ends.

**How it works:** Python's built-in `open()` function is the entry point for all file operations — reading, writing, or appending.

```python
file = open("example.txt", "w")   # opens (or creates) a file for writing
file.write("Hello, file!")
file.close()                       # always close when done
```

---

### 2. File Operations in Python
**What it does:** Defines the different "modes" you can open a file in, depending on what you want to do with it.

**How it works:**
- `"r"` — read (default; file must exist)
- `"w"` — write (creates new file, **overwrites** if it exists)
- `"a"` — append (adds to the end, doesn't erase existing content)
- `"rb"` / `"wb"` — same as above but in binary mode

```python
f1 = open("data.txt", "r")   # read mode
f2 = open("data.txt", "w")   # write mode (overwrites!)
f3 = open("data.txt", "a")   # append mode (adds to end)
```

---

### 3. `with open`
**What it does:** The recommended way to work with files — automatically closes the file for you, even if an error happens mid-way.

**How it works:** `with` creates a temporary block; once the block ends (or an error is raised inside it), the file is closed automatically. No need to manually call `.close()`.

```python
with open("notes.txt", "w") as f:
    f.write("Hello!")
# file is automatically closed here, even if something went wrong above
```

---

### 4. Writing a File
**What it does:** Saves text content into a file.

**How it works:** Open in `"w"` mode, then use `.write()` for a single string, or `.writelines()` for a list of strings.

```python
with open("notes.txt", "w") as f:
    f.write("Line 1\n")
    f.write("Line 2\n")

lines = ["Line A\n", "Line B\n"]
with open("notes2.txt", "w") as f:
    f.writelines(lines)
```

---

### 5. Reading a File
**What it does:** Loads the content of an existing file back into your program.

**How it works:**
- `.read()` — reads the whole file as one string.
- `.readline()` — reads a single line at a time.
- `.readlines()` — reads all lines into a list.
- Looping directly over the file object reads it line by line (memory-efficient).

```python
with open("notes.txt", "r") as f:
    content = f.read()
    print(content)         # entire file as one string

with open("notes.txt", "r") as f:
    for line in f:          # memory-efficient, one line at a time
        print(line.strip())
```

---

### 6. Handling Binary Files
**What it does:** Lets you read/write non-text files — images, PDFs, videos — where content isn't plain text characters.

**How it works:** Use `"rb"` (read binary) or `"wb"` (write binary) modes. Data is handled as raw bytes instead of strings.

```python
# Copying an image file in binary mode
with open("photo.jpg", "rb") as source:
    data = source.read()

with open("photo_copy.jpg", "wb") as destination:
    destination.write(data)
```

---

### 7. Appending in a File
**What it does:** Adds new content to the **end** of an existing file, without deleting what's already there.

**How it works:** Use `"a"` mode — unlike `"w"`, it doesn't erase existing content; it just moves the "cursor" to the end before writing.

```python
with open("log.txt", "a") as f:
    f.write("New log entry\n")

# Run this multiple times -> each run ADDS a new line, doesn't overwrite
```

---

## MODULE 16: Error & Exception Handling

### 1. Intro to Errors & Exceptions in Python
**What it does:** Explains the difference between a program crashing outright and handling problems gracefully.

**How it works:** An **error** stops your program immediately (like a typo — `SyntaxError`). An **exception** is a runtime problem (like dividing by zero) that you *can* catch and handle so the program keeps running.

```python
# This crashes with a SyntaxError - can't be "caught"
# print("Hello"

# This is a runtime exception - CAN be caught and handled
print(10 / 0)   # ZeroDivisionError: division by zero
```

---

### 2. Try & Except
**What it does:** Lets you attempt risky code and define what happens if it fails, instead of crashing the whole program.

**How it works:** Code that might fail goes inside `try`. If an exception occurs, Python immediately jumps to the matching `except` block instead of crashing.

```python
try:
    num = int(input("Enter a number: "))
    print(10 / num)
except:
    print("Something went wrong!")
```

---

### 3. Except Block
**What it does:** Lets you handle **specific** types of errors differently, instead of catching everything the same way.

**How it works:** You can chain multiple `except` blocks, each targeting a specific exception type. Python checks them top to bottom and runs the first one that matches.

```python
try:
    num = int(input("Enter a number: "))
    print(10 / num)
except ZeroDivisionError:
    print("Can't divide by zero!")
except ValueError:
    print("That wasn't a valid number!")
except Exception as e:          # catches anything else
    print(f"Unexpected error: {e}")
```

---

### 4. Finally in Python
**What it does:** Runs cleanup code that must execute **no matter what** — whether an error happened or not.

**How it works:** The `finally` block always runs last, after `try`/`except` finish, even if an exception was raised and not caught. Commonly used to close files or release resources.

```python
try:
    f = open("data.txt", "r")
    print(f.read())
except FileNotFoundError:
    print("File not found!")
finally:
    print("Cleanup: closing resources")   # ALWAYS runs
    # f.close() would go here in real code
```

---

## Quick Reference Cheat Sheet

| Concept | One-line takeaway |
|---|---|
| `__init__` | Constructor — runs automatically when an object is created |
| Class variable | Shared across ALL objects of a class |
| Instance variable (`self.x`) | Unique to each individual object |
| `super()` | Calls the parent class's version of a method |
| Method override | Child class redefines a method with the same name |
| `with open(...)` | Auto-closes files, even on error — always prefer this |
| `"r" / "w" / "a"` | Read / Write (overwrites) / Append (adds to end) |
| `try/except/finally` | Attempt risky code / handle failure / always cleanup |

---

*Tip: For OOP, try modeling something from your own life (a `Rupeer` transaction, a `BusStop`, a `Student`) — designing your own class from scratch cements the concept far better than copying examples.*