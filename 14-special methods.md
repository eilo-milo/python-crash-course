

---

# Object-Oriented Programming: Special (Dunder / Magic) Methods & Operator Overloading

---

## 1. What Are Special (Dunder) Methods?
* Special methods—also referred to as **magic methods** or **dunder methods**—are surrounded by leading and trailing double underscores (e.g., `__init__`).
* They allow custom user-defined classes to emulate built-in language behaviors and provide customized implementations for standard operations (operator overloading).
* Calling standard operators or built-in functions (such as `+`, `len()`, `print()`, or `str()`) invokes their corresponding dunder method implicitly behind the scenes.

---

## 2. String Representation Methods
By default, printing a custom class instance outputs an uninformative string displaying its memory address (e.g., `<__main__.Employee object at 0x...>`). Implementing string representation methods makes instances readable and informative.

### 2.1 `__repr__`: Unambiguous Developer Representation
* Aimed at developers for debugging and logging.
* **Best practice guideline**: Return a formatted string that mirrors the exact Python expression required to recreate the object.
* Acts as the automatic fallback if `__str__` is not defined on the class.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def __repr__(self):
        return f"Employee('{self.first}', '{self.last}', {self.pay})"

emp_1 = Employee('Corey', 'Schafer', 50000)
print(repr(emp_1))  # Output: Employee('Corey', 'Schafer', 50000)
```

### 2.2 `__str__`: Readable End-User Representation
* Aimed at end users to display intuitive, readable summaries.
* Invoked automatically when an instance is passed to `print(instance)` or `str(instance)`.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def fullname(self):
        return f"{self.first} {self.last}"

    def __repr__(self):
        return f"Employee('{self.first}', '{self.last}', {self.pay})"

    def __str__(self):
        return f"{self.fullname()} - {self.first}.{self.last}@company.com"

emp_1 = Employee('Corey', 'Schafer', 50000)
print(emp_1)  # Output: Corey Schafer - Corey.Schafer@company.com
```

### 2.3 Direct Calling vs. Built-in Functions
Built-in top-level functions map directly to underlying dunder methods:
* `repr(emp_1)` is equivalent to `emp_1.__repr__()`
* `str(emp_1)` is equivalent to `emp_1.__str__()`

---

## 3. Operator Overloading & Arithmetic Methods

### 3.1 Overloading Addition with `__add__`
* The addition operator (`+`) evaluates differently depending on the operand types: integers invoke `int.__add__(1, 2)` (arithmetic sum), while strings invoke `str.__add__('a', 'b')` (concatenation).
* Implementing `__add__(self, other)` on a custom class allows objects of that type to define their own addition logic.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def __add__(self, other):
        if isinstance(other, Employee):
            return self.pay + other.pay
        return NotImplemented

emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'User', 60000)

print(emp_1 + emp_2)  # Output: 110000
```

### 3.2 Returning `NotImplemented`
* When an overloaded operator does not know how to handle the operand type passed in as `other`, returning `NotImplemented` instead of raising an error signals to Python to fall back on the other operand's reflected method (e.g., `__radd__`) before raising a `TypeError`.

---

## 4. Emulating Built-in Functions (`__len__`)
* The built-in `len()` function calls an object's `__len__()` method behind the scenes (`len('test')` is identical to `'test'.__len__()`).
* Implementing `__len__` enables instances to return meaningful size measurements.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def fullname(self):
        return f"{self.first} {self.last}"

    def __len__(self):
        return len(self.fullname())

emp_1 = Employee('Corey', 'Schafer', 50000)
print(len(emp_1))  # Output: 13 (character count of "Corey Schafer")
```

---

## 5. Standard Library Case Study (`datetime`)
* **`timedelta` addition (`__add__`)**: Combines two `timedelta` objects by adding their internal `days`, `seconds`, and `microseconds` fields. If added against an incompatible type, it returns `NotImplemented`.
* **`date` representation (`__repr__`)**: Returns formatted source code (e.g., `datetime.date(2016, 7, 24)`) so developers can recreate the object.
* **`date` string representation (`__str__`)**: Points directly to `date.isoformat()`, ensuring default `print()` statements yield standardized ISO dates (`YYYY-MM-DD`).

---
