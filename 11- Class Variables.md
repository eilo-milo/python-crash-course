---

# Object-Oriented Programming: Class Variables

---

## 1. Instance Variables vs. Class Variables
* **Instance Variables**: Data distinct to each unique instance, typically assigned using `self.variable = value` inside the `__init__` constructor method (e.g., individual employee names, unique emails, specific base salaries).
* **Class Variables**: Variables shared universally across all instances of a class; the data point remains identical unless explicitly overridden.

---

## 2. Defining and Accessing Class Variables

### 2.1 Defining Class Attributes
* Class variables are declared directly inside the class definition body, outside any internal methods.

```python
class Employee:
    # Class variable
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@company.com"

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)
```

### 2.2 Access Rules: Class Name vs. `self`
* Class variables cannot be referenced as bare identifier names (writing `raise_amount` inside a method body triggers a `NameError: name 'raise_amount' is not defined`).
* They must always be accessed via either:
  1. The class directly: `Employee.raise_amount`
  2. The instance: `self.raise_amount` or `emp_1.raise_amount`

---

## 3. Namespace Lookup Mechanics (`__dict__`)

### 3.1 How Attribute Resolution Works
When accessing an attribute on an instance (e.g., `emp_1.raise_amount`), Python resolves it in a strict search hierarchy:
1. Checks the **instance namespace** to determine if the attribute exists on that specific object.
2. If absent, searches the **class namespace** from which the object was instantiated.
3. If absent, continues searching up the inheritance tree across parent superclasses.

### 3.2 Inspecting Namespaces with `__dict__`
* The `__dict__` attribute returns a dictionary containing the local namespace of an instance or class.
* Newly instantiated objects do not contain class variables within their own `__dict__`; they retrieve the attribute by referencing the class namespace.

```python
emp_1 = Employee('Corey', 'Schafer', 50000)

print(emp_1.__dict__)
# Contains: {'first': 'Corey', 'last': 'Schafer', 'pay': 50000, 'email': '...'}
# Note: 'raise_amount' is absent from the instance namespace

print(Employee.__dict__)
# Contains: {'raise_amount': 1.04, ...}
```

---

## 4. Mutating Class Variables

### 4.1 Modifying via the Class (`Employee.raise_amount`)
* Reassigning the variable using the class name updates the value globally across the class and all listening instances that have not overridden it.

```python
Employee.raise_amount = 1.05

print(Employee.raise_amount)  # 1.05
print(emp_1.raise_amount)     # 1.05
print(emp_2.raise_amount)     # 1.05
```

### 4.2 Overriding via an Instance (`emp_1.raise_amount`)
* Assigning a value to a class variable through an instance does **not** alter the class variable.
* Instead, it creates a new **instance attribute** within that specific object's local namespace, shadowing the class-level variable.

```python
emp_1.raise_amount = 1.06

print(Employee.raise_amount)  # 1.05 (unchanged)
print(emp_1.raise_amount)     # 1.06 (overridden in emp_1's namespace)
print(emp_2.raise_amount)     # 1.05 (falls back to class value)

print(emp_1.__dict__)         # Now contains 'raise_amount': 1.06
```

### 4.3 Design Decision: When to Reference `self` vs. `ClassName`
* **Using `self.variable`**: Recommended when child subclasses or individual instances need the flexibility to override the default value (e.g., setting a customized raise percentage for a single employee).
* **Using `ClassName.variable`**: Recommended when the value must strictly remain constant and synchronized across all instances without allowing instance-level overrides.

---

## 5. Class-Wide Counters (`num_of_employees`)
* Tracking total instance counts or shared registry states requires updating the attribute strictly through the class name inside `__init__`.
* Referencing `self.num_of_employees += 1` would create an isolated instance attribute rather than incrementing a shared counter.

```python
class Employee:
    num_of_employees = 0
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@company.com"

        # Explicitly increment via the class
        Employee.num_of_employees += 1

print(Employee.num_of_employees)  # Output: 0

emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'User', 60000)

print(Employee.num_of_employees)  # Output: 2
```

---
