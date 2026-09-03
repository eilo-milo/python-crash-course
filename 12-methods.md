

---

# Object-Oriented Programming: Regular Methods, Class Methods, and Static Methods


---

## 1. Method Types Comparison

| Method Type | Decorator | First Argument | Automatically Passed Entity | Primary Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Regular Method** | None | `self` | The calling object instance | Operating on or altering instance-specific state. |
| **Class Method** | `@classmethod` | `cls` | The class itself | Altering class-wide state or building alternative constructors. |
| **Static Method** | `@staticmethod` | None | Nothing | Self-contained utilities with a logical relationship to the class. |

---

## 2. Regular Instance Methods
* Regular methods defined in a class automatically receive the calling instance as their first positional argument (`self`).
* They read and mutate instance variables (e.g., `self.pay`, `self.first`).

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)
```

---

## 3. Class Methods (`@classmethod`)

### 3.1 Defining and Mutating Class State
* Declared with the `@classmethod` decorator.
* Receives the class object as the first parameter by convention named `cls` (`class` cannot be used because it is a reserved Python keyword).
* Can be executed directly from the class (e.g., `Employee.set_raise_amount(1.05)`) or through an instance, modifying the class variable across all instances.

```python
class Employee:
    num_of_employees = 0
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount

# Calling on the class directly
Employee.set_raise_amount(1.05)
print(Employee.raise_amount)  # Output: 1.05
```

### 3.2 Class Methods as Alternative Constructors
* Class methods provide alternate interfaces for instantiating objects from diverse raw input formats (such as delimited strings, JSON dictionaries, or tuples).
* Conventionally named starting with `from_` (e.g., `from_string`).
* They parse the source data, invoke `cls(...)` to construct the instance, and return the newly formed object.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, int(pay))

# Raw input data
emp_str_1 = 'John-Doe-70000'

# Instantiate directly via alternative constructor
new_emp = Employee.from_string(emp_str_1)
print(new_emp.first)  # Output: John
print(new_emp.pay)    # Output: 70000
```

### 3.3 Real-World Example: `datetime.fromtimestamp`
* Python's standard library `datetime` module utilizes class methods as alternative constructors:
  * Default constructor: `datetime.date(year, month, day)`
  * Alternative class method constructor: `datetime.date.fromtimestamp(timestamp)`

---

## 4. Static Methods (`@staticmethod`)

### 4.1 Purpose and Behavior
* Declared using the `@staticmethod` decorator.
* Do **not** pass `self` or `cls` automatically.
* Behave identical to standard standalone functions, but are enclosed inside a class namespace because they have a clear logical connection to that class.

### 4.2 Implementation Example: Workday Checker
* Python's `.weekday()` method returns integers representing days of the week (`0` = Monday, ..., `5` = Saturday, `6` = Sunday).

```python
import datetime

class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    @staticmethod
    def is_workday(day):
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True

# Testing dates
my_date_sunday = datetime.date(2016, 7, 10)
my_date_monday = datetime.date(2016, 7, 11)

print(Employee.is_workday(my_date_sunday))  # Output: False
print(Employee.is_workday(my_date_monday))  # Output: True
```

### 4.3 Identifying When to Use Static Methods
* **Heuristic**: If a method within a class does not reference `self` (instance state) and does not reference `cls` (class state), it should typically be designated as a `@staticmethod`.

---
