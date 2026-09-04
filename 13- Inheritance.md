
---

# Object-Oriented Programming: Class Inheritance and Subclasses


---

## 1. Understanding Inheritance
* Inheritance allows a class to derive attributes and methods from an existing parent class.
* Promotes code reuse and adheres to DRY (Don't Repeat Yourself) principles by isolating shared logic in a parent class while allowing subclasses to override or extend functionality independently.
* A subclass is defined by passing the parent class name inside parentheses after the subclass name: `class Subclass(ParentClass):`.

```python
class Employee:
    raise_amount = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = f"{first}.{last}@company.com"

    def fullname(self):
        return f"{self.first} {self.last}"

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)

class Developer(Employee):
    pass

# Developer instances automatically inherit all Employee attributes and methods
dev_1 = Developer('Corey', 'Schafer', 50000)
print(dev_1.email)  # Corey.Schafer@company.com
```

---

## 2. Method Resolution Order (MRO) & `help()`
* When an attribute or method is requested, Python searches along the **Method Resolution Order (MRO)**:
  1. The instance's own class.
  2. Direct parent superclasses in order of inheritance.
  3. The base `object` class (the ultimate ancestor of all Python classes).
* Passing a class into `help(ClassName)` prints out its MRO, inherited methods, and class attributes.

```python
print(help(Developer))
# Method Resolution Order:
#  Developer
#  Employee
#  builtins.object
```

---

## 3. Customizing Subclasses

### 3.1 Overriding Class Attributes
* Redefining an attribute inside a subclass alters its value solely for that subclass and its instances, leaving the parent class and sister subclasses completely untouched.

```python
class Developer(Employee):
    raise_amount = 1.10  # Overrides the 1.04 value from Employee

dev_1 = Developer('Corey', 'Schafer', 50000)
emp_1 = Employee('Test', 'User', 50000)

dev_1.apply_raise()
emp_1.apply_raise()

print(dev_1.pay)  # Output: 55000 (10% increase)
print(emp_1.pay)  # Output: 52000 (4% increase)
```

### 3.2 Extending `__init__` with `super()`
* When a subclass requires unique initialization arguments (e.g., `prog_lang`), use `super().__init__(...)` to delegate shared parameter initialization to the parent class constructor.
* `super()` ensures cleaner maintenance and scalability, especially when moving to multiple inheritance architectures.

```python
class Developer(Employee):
    raise_amount = 1.10

    def __init__(self, first, last, pay, prog_lang):
        super().__init__(first, last, pay)
        self.prog_lang = prog_lang

dev_1 = Developer('Corey', 'Schafer', 50000, 'Python')
print(dev_1.email)      # Set by Employee.__init__
print(dev_1.prog_lang)  # Set by Developer.__init__
```

---

## 4. Complex Subclass Implementation (`Manager`)

### 4.1 Avoiding Mutable Default Arguments
* **Critical Rule**: Never pass mutable data types (such as empty lists `[]` or dictionaries `{}`) as default parameter values.
* Because default arguments are evaluated once when the function is defined, a mutable default will be shared across all instances that omit the argument.
* Instead, set the default parameter to `None` and initialize an empty list inside the method body.

```python
class Manager(Employee):
    def __init__(self, first, last, pay, employees=None):
        super().__init__(first, last, pay)
        if employees is None:
            self.employees = []
        else:
            self.employees = employees
```

### 4.2 Managing Associated Objects via Methods
* Subclasses can contain custom behaviors to mutate internal collections of other instantiated objects.

```python
class Manager(Employee):
    def __init__(self, first, last, pay, employees=None):
        super().__init__(first, last, pay)
        if employees is None:
            self.employees = []
        else:
            self.employees = employees

    def add_emp(self, emp):
        if emp not in self.employees:
            self.employees.append(emp)

    def remove_emp(self, emp):
        if emp in self.employees:
            self.employees.remove(emp)

    def print_emps(self):
        for emp in self.employees:
            print('-->', emp.fullname())

dev_1 = Developer('Corey', 'Schafer', 50000, 'Python')
dev_2 = Developer('Test', 'Employee', 60000, 'Java')

mgr_1 = Manager('Sue', 'Smith', 90000, [dev_1])
mgr_1.add_emp(dev_2)
mgr_1.print_emps()
```

---

## 5. Type Inspection: `isinstance()` and `issubclass()`

### 5.1 Checking Object Types with `isinstance()`
* `isinstance(object, Class)` verifies whether an instantiated object is an instance of a specific class or any class along its inheritance chain.

```python
print(isinstance(mgr_1, Manager))    # True
print(isinstance(mgr_1, Employee))   # True (inherited)
print(isinstance(mgr_1, Developer))  # False
```

### 5.2 Checking Class Trees with `issubclass()`
* `issubclass(ChildClass, ParentClass)` verifies whether a target class inherits directly or indirectly from another class.

```python
print(issubclass(Developer, Employee))  # True
print(issubclass(Manager, Employee))    # True
print(issubclass(Manager, Developer))   # False
```

---

## 6. Real-World Application (Exception Hierarchies)
* Real-world Python libraries rely on inheritance to construct cleanly organized error hierarchies.
* In web servers and WSGI frameworks (such as Werkzeug), generic base exceptions like `HTTPException` provide broad status handling logic, while concrete child exceptions (`BadRequest`, `NotFound`, `Unauthorized`) inherit from the base and simply update HTTP response codes and descriptions.

---
