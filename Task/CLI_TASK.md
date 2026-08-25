# Task: Extend the Employee Payroll Console App

**Level:** Level 1 (beginner)
**Time budget:** 2 hours max
**Goal:** Prove you understand the `Employee` -> `ModifiedIntern` / `ModifiedManager` / `ModifiedDevelopers` hierarchy by *using* it, not just reading it - polymorphism, encapsulation, and working within an existing class design instead of hacking around it.

---

## Task A - Find Employee by ID

### What problem are we facing currently?
The CLI tool can add Managers, Developers, and Interns, and it can print the *entire* list or the total payroll. But if someone wants to check a single employee's details, there's no way to do it - the only option is to print all employees and scroll through the list until you spot the right one. That doesn't scale once there are more than a handful of employees.

### Why do we need to add this?
Looking up one record by ID is one of the most basic things any data-management tool needs to do. Right now `Main` only ever adds to the list and reads the whole list - it never looks something up. Without a search, every "what's employee #104's salary?" question means manually scanning output, which is slow and error-prone.

### How is it done?
- Add a new private method in `Main`, e.g. `findEmployeeById()`, wired into `printMenu()`'s switch statement as option 6.
- Loop through the `employees` list, compare each `Employee`'s ID to the one entered.
- When a match is found, call `.printDetails()` on it - **don't** write `instanceof` checks to figure out what subclass it is first. Because `printDetails()` is overridden in each subclass, calling it on an `Employee`-typed reference automatically runs the correct version (polymorphism). If you find yourself branching on the type, you're fighting the design instead of using it.
- If the loop finishes with no match, print a "not found" message instead of crashing.

### Sample output - before and after

**Before (feature doesn't exist yet):**
```
Enter choice: 6
Exception in thread "main" java.util.NoSuchElementException
(option 6 isn't wired up, so this either crashes or falls to "Invalid choice")
```

**After (feature implemented):**
```
Enter choice: 6
Enter Employee ID to search: 104

--- Employee Found ---
ID: 104
Name: Priya S
Role: Developer
Salary: 47500.0
```
```
Enter choice: 6
Enter Employee ID to search: 999

No employee found with ID: 999
```

### How would it impact the system?
Purely additive - no existing menu option, class, or field changes. `Employee` and its subclasses don't need any new code at all, since `printDetails()` already exists and is already overridden correctly. The only new code lives in `Main`. This also becomes the foundation Task B reuses (finding an employee before modifying their salary), so getting this one right first makes the second task easier.

---

## Task B - Give an Employee a Raise

### What problem are we facing currently?
There's no way to change an employee's salary after they're added. `baseSalary` is set once in the constructor and never touched again - so a real, everyday HR action ("this developer finished a big project, give them a Rs.5,000 raise") simply can't be done through the tool.

### Why do we need to add this?
A payroll tool that can only ever set salary once isn't very useful in practice - salaries change. But *how* this gets added matters as much as *whether* it does: `baseSalary` is `private` for a reason, and the fix shouldn't be to make it public or to bolt on an unchecked setter that would let someone set a negative salary by mistake.

### How is it done?
- In `Employee.java`, add a method like `public void giveRaise(double amount)` that adds `amount` to `baseSalary`, but only after checking `amount` is positive. This keeps `baseSalary` `private` - the *only* way to change it is through a method the class itself controls and guards.
- In `Main.java`, add option 7: find the employee by ID (reuse Task A's search logic), then call `.giveRaise(amount)` on the result.
- Because the guard lives inside `Employee`, every subclass (`ModifiedIntern`, `ModifiedManager`, `ModifiedDevelopers`) gets the same protection automatically, without repeating the check anywhere else.

### Sample output - before and after

**Before (feature doesn't exist yet):**
```
Enter choice: 7
(option 7 isn't wired up - falls through to "Invalid choice".
 Even trying employee.baseSalary = ... directly from Main wouldn't
 compile, since baseSalary is private.)
```

**After (feature implemented):**
```
Enter choice: 7
Enter Employee ID: 104
Enter raise amount: 5000

Raise applied. New salary for Priya S: 52500.0
```
```
Enter choice: 7
Enter Employee ID: 104
Enter raise amount: -1000

Raise amount must be positive. No changes made.
```

### How would it impact the system?
`Employee` gains one new method; no existing method signatures change, so nothing that currently compiles breaks. Salary can now go up after an employee is added, and any code elsewhere that reads `baseSalary` (like total payroll) automatically reflects the new value on the next read, since it's the same field, just updated in place. The negative-amount guard means the system can't end up in an invalid state (negative salary) no matter which subclass the employee belongs to.

---

## What "Done" Looks Like

- [ ] Menu shows options 1-7, old options still work unchanged
- [ ] Option 6 finds an existing employee and prints correct role-specific details via `printDetails()` - no `instanceof` chains
- [ ] Option 6 handles an ID that doesn't exist without crashing
- [ ] Option 7 raises salary through a method on `Employee`, not a public field
- [ ] Option 7 rejects a negative raise amount with a message, doesn't crash or silently apply it
- [ ] You can explain out loud *why* `giveRaise()` lives in `Employee` and not in each subclass separately

If you finish early: think about (don't need to implement) what would need to change if `Manager` needed a *different* raise rule than `Developer` - e.g. managers' raises also bump their bonus by 10%. Where would that logic go, and why?
