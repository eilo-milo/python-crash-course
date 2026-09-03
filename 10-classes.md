

---

# Object-Oriented Programming: Classes and Instances


---

## 1. Why Use Classes?
* Classes allow logical grouping of data and functions into reusable, extensible blueprints.
* **Attributes**: Data and variables associated with a class or instance.
* **Methods**: Functions defined inside a class that operate on its instances.

---

## 2. Classes vs. Instances
* **Class**: The blueprint/template defining the structure, properties, and behaviors.
* **Instance**: An individual, concrete object created from the blueprint.
* Multiple instances created from the same class occupy distinct, unique addresses in system memory.
* An empty class can be defined using the `pass` placeholder statement to avoid syntax errors during initial setup.

```python
class Employee:
    pass

emp_1 = Employee()
emp_2 = Employee()

print(emp_1)  # <__main__.Employee object at 0x...>
print(emp_2)  # <__main__.Employee object at 0x...>
```

---

## 3. Manual Instance Attribute Assignment
* Attributes can be attached to instances manually on the fly.
* **Drawback**: Highly repetitive, produces verbose code, and easily leads to variable mismatch errors across different instances.

```python
emp_1 = Employee()
emp_2 = Employee()

# Manually assigning attributes
emp_1.first = 'Corey'
emp_1.last = 'Schafer'
emp_1.email = 'Corey.Schafer@company.com'
emp_1.pay = 50000

emp_2.first = 'Test'
emp_2.last = 'User'
emp_2.email = 'Test.User@company.com'
emp_2.pay = 60000
```

---

## 4. The `__init__` Initialization Method

### 4.1 Purpose and Role of `self`
* The `__init__` method serves as the class constructor / initializer that runs automatically every time a new instance is created.
* By convention, the first parameter is named `self`.
* `self` represents the specific instance being instantiated, automatically passed into the method by Python.

### 4.2 Initializing Instance Attributes
* Arguments passed to the class call are mapped to `__init__` parameters and assigned directly to the instance via `self.attribute = value`.
* Derived attributes (such as email addresses constructed from names) can be generated dynamically within `__init__`.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@company.com"

# Creating instances automatically populates attributes
emp_1 = Employee('Corey', 'Schafer', 50000)
emp_2 = Employee('Test', 'User', 60000)

print(emp_1.email)  # Corey.Schafer@company.com
print(emp_2.email)  # Test.User@company.com
```

---

## 5. Adding Methods to a Class

### 5.1 Defining and Calling Methods
* Regular methods defined within a class must accept `self` as their first parameter so they can access the data belonging to that specific instance.

```python
class Employee:
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@company.com"

    def fullname(self):
        return f"{self.first} {self.last}"

emp_1 = Employee('Corey', 'Schafer', 50000)
print(emp_1.fullname())  # Output: Corey Schafer
```

### 5.2 Attributes vs. Methods: The Parentheses Rule
* **Attributes** store data and do not take parentheses: `emp_1.first`.
* **Methods** perform actions and require parentheses `()` to execute: `emp_1.fullname()`.
* Omitting parentheses on a method call (`emp_1.fullname`) returns the method object reference rather than executing the function.

---

## 6. Common Errors & Behind-the-Scenes Mechanics

### 6.1 Omitting `self` (`TypeError`)
* Forgetting `self` in a method definition causes a runtime exception when invoked on an instance:
  ```text
  TypeError: fullname() takes 0 positional arguments but 1 was given
  ```
* Even if the method call looks empty (`emp_1.fullname()`), Python passes the calling instance behind the scenes as the first positional argument.

### 6.2 Calling Methods from Instance vs. Class
Calling a method from an instance is shorthand for calling the method on the class and passing the instance explicitly:

```python
# Instance call (passes emp_1 to self automatically):
emp_1.fullname()

# Class call (must pass instance manually):
Employee.fullname(emp_1)
```

Both invocations are functionally identical, but calling via the instance is the standard practice.

---
