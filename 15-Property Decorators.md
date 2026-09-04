

---

# Object-Oriented Programming: Property Decorators (Getters, Setters, and Deleters)

---

## 1. Motivation: The Dynamic Attribute Problem
* When attributes are derived from other attributes inside `__init__` (e.g., generating `self.email = f"{first}.{last}@email.com"`), mutating a constituent component (like `emp_1.first = 'Jim'`) leaves the dependent attribute out of sync with stale data.
* Converting the dependent attribute into a regular method (`def email(self):`) solves the synchronization issue, but breaks backward compatibility because every existing consumer must update syntax from `emp_1.email` to `emp_1.email()`.

---

## 2. The `@property` Decorator (Getter)
* Decorating a method with `@property` allows it to be accessed using standard attribute syntax without parentheses (`emp_1.email` instead of `emp_1.email()`).
* Acts as a **getter**: dynamic logic executes behind the scenes on every access, ensuring current state resolution while preserving an attribute-style public interface.

```python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return f"{self.first}.{self.last}@email.com"

    @property
    def fullname(self):
        return f"{self.first} {self.last}"

emp_1 = Employee('John', 'Smith')
emp_1.first = 'Jim'

# Accessed like attributes, yet evaluate dynamically
print(emp_1.first)     # Jim
print(emp_1.email)     # Jim.Smith@email.com
print(emp_1.fullname)  # Jim Smith
```

---

## 3. Implementing Setters (`@property_name.setter`)
* Attempting direct assignment on a property decorated method (e.g., `emp_1.fullname = 'Corey Schafer'`) without an explicit setter raises an `AttributeError: can't set attribute`.
* A setter is created using `@<property_name>.setter` above a method sharing the exact same name as the property.
* The setter accepts the incoming assigned value, parses/validates it, and mutates underlying instance attributes accordingly.

```python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def fullname(self):
        return f"{self.first} {self.last}"

    @fullname.setter
    def fullname(self, name):
        first, last = name.split(' ')
        self.first = first
        self.last = last

emp_1 = Employee('John', 'Smith')

# Invokes the @fullname.setter
emp_1.fullname = 'Corey Schafer'

print(emp_1.first)     # Corey
print(emp_1.last)      # Schafer
print(emp_1.fullname)  # Corey Schafer
```

---

## 4. Implementing Deleters (`@property_name.deleter`)
* Defined using `@<property_name>.deleter` over a method with the matching property name.
* Triggers when the Python `del` statement targets the attribute: `del emp_1.fullname`.
* Primarily used for cleanup actions, nullifying dependent instance references, or state resetting.

```python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def fullname(self):
        return f"{self.first} {self.last}"

    @fullname.deleter
    def fullname(self):
        print("Delete Name!")
        self.first = None
        self.last = None

emp_1 = Employee('Corey', 'Schafer')

# Invokes the @fullname.deleter
del emp_1.fullname

print(emp_1.first)  # None
print(emp_1.last)   # None
```

---

## 5. API Stability and Backward Compatibility
* In Python, exposing simple public attributes directly (`self.first`, `self.last`) is idiomatic.
* When requirements evolve to require validation, parsing, or dynamic recalculation, `@property` allows methods to wrap attribute access transparently without breaking existing external call sites or client code.

---

