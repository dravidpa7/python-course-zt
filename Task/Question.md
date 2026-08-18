# OOP Coding Tasks — Inheritance, Polymorphism, Abstraction (Medium)

---

## Task 1 — Inheritance: Employee Management

**Problem:**
Create a base class `Employee` with `name` and `salary`. Create two child classes:
- `Manager` — adds `team_size`, and a method `details()` that returns name, salary, and team size.
- `Developer` — adds `programming_language`, and a method `details()` that returns name, salary, and language.

Both `details()` methods should reuse the parent's data (via `super()` or direct access), not repeat name/salary logic from scratch.

**Sample Input:**
```python
m = Manager("Asha", 80000, 5)
d = Developer("Ravi", 60000, "Python")

print(m.details())
print(d.details())
```

**Sample Output:**
```
Asha earns 80000 and manages a team of 5
Ravi earns 60000 and codes in Python
```
---

## Task 2 — Polymorphism: Shape Area Calculator

**Problem:**
Create a base class `Shape` with a method `area()` that returns `0`. Create child classes `Rectangle` and `Triangle`, each overriding `area()` with their own formula. Then write a function `total_area(shapes)` that takes a **list** of shape objects and returns the sum of all their areas — it should work no matter what mix of shapes is passed in, without checking each object's type.

**Sample Input:**
```python
shapes = [Rectangle(4, 5), Triangle(6, 3), Rectangle(2, 2)]
print(total_area(shapes))

for s in shapes:
    print(s.area())
```

**Sample Output:**
```
33.0
20
9.0
4
```
*(Rectangle: 4×5=20, Triangle: 0.5×6×3=9.0, Rectangle: 2×2=4 → total = 33.0)*

---

## Task 3 — Abstraction: Payment System

**Problem:**
Using the `abc` module, create an abstract class `Payment` with an abstract method `pay(amount)`. Create two concrete classes `UPI` and `CreditCard` that implement `pay()` differently. Then write a function `process_payment(payment_method, amount)` that calls `.pay(amount)` on whatever payment object is passed in — the function itself should have no idea which payment type it's dealing with.

**Sample Input:**
```python
upi = UPI()
cc = CreditCard()

process_payment(upi, 1500)
process_payment(cc, 2500)

p = Payment()   # try to instantiate the abstract class directly
```

**Sample Output:**
```
Paid 1500 using UPI
Paid 2500 using Credit Card
TypeError: Can't instantiate abstract class Payment with abstract method pay
```
---
