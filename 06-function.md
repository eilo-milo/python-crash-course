
---

# Chapter 08: Functions

---

## 1. Defining a Function

### 1.1 Syntax and Docstrings
* Functions are defined using the `def` keyword, followed by the function name, parentheses `()`, and a colon `:`.
* A **docstring** enclosed in triple quotation marks (`"""..."""`) immediately follows the header line to document the function's intended purpose.

```python
def greet_user():
    """Display a simple greeting."""
    print("Hello!")

greet_user()
```

### 1.2 Parameters vs. Arguments
* **Parameter**: A variable listed inside the parentheses of a function definition.
* **Argument**: A concrete value passed into the function during a function call.

```python
def greet_user(username):  # username is a parameter
    """Display a personalized greeting."""
    print(f"Hello, {username.title()}!")

greet_user('jesse')        # 'jesse' is an argument
```

---

## 2. Passing Arguments

### 2.1 Positional Arguments
* Matches passed arguments to parameters sequentially based on the order in which they are supplied.
* Mixing up argument ordering results in semantic or runtime bugs.

```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
```

### 2.2 Keyword Arguments
* Passes name-value pairs explicitly in the call statement (`parameter_name=value`), removing reliance on positional ordering.

```python
describe_pet(animal_type='hamster', pet_name='harry')
describe_pet(pet_name='harry', animal_type='hamster')
```

### 2.3 Default Parameter Values
* Parameters can define a fallback default value in the header.
* Parameters with default values must always follow all positional parameters without defaults in the definition header.

```python
def describe_pet(pet_name, animal_type='dog'):
    """Display information about a pet with a default type."""
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet('willie')                         # Uses default 'dog'
describe_pet(pet_name='harry', animal_type='hamster')  # Overrides default
```

### 2.4 Avoiding Argument Errors
* Passing fewer or more arguments than required triggers a `TypeError` indicating the missing positional arguments.

---

## 3. Return Values

### 3.1 Returning Single and Formatted Values
* The `return` statement sends a computed value back to the line where the function was called.

```python
def get_formatted_name(first_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = f"{first_name} {last_name}"
    return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician)  # Output: Jimi Hendrix
```

### 3.2 Making Arguments Optional
* Setting an optional parameter's default value to an empty string `''` or `None` allows calling the function with varying argument combinations.

```python
def get_formatted_name(first_name, last_name, middle_name=''):
    """Return a full name, neatly formatted with an optional middle name."""
    if middle_name:
        full_name = f"{first_name} {middle_name} {last_name}"
    else:
        full_name = f"{first_name} {last_name}"
    return full_name.title()

print(get_formatted_name('jimi', 'hendrix'))
print(get_formatted_name('john', 'hooker', 'lee'))
```

### 3.3 Returning Data Structures (Dictionaries)
* Functions can package multiple pieces of input data into dictionaries or lists before returning.

```python
def build_person(first_name, last_name, age=''):
    """Return a dictionary of information about a person."""
    person = {'first': first_name, 'last': last_name}
    if age:
        person['age'] = age
    return person

musician = build_person('jimi', 'hendrix', age=27)
print(musician)  # Output: {'first': 'jimi', 'last': 'hendrix', 'age': 27}
```

### 3.4 Using Functions with `while` Loops
* Functions integrate cleanly inside control loops to encapsulate processing logic.

```python
while True:
    print("\nPlease tell me your name (or 'q' to quit):")
    f_name = input("First name: ")
    if f_name == 'q':
        break
    l_name = input("Last name: ")
    if l_name == 'q':
        break
        
    formatted_name = get_formatted_name(f_name, l_name)
    print(f"\nHello, {formatted_name}!")
```

---

## 4. Passing and Modifying Lists

### 4.1 Modifying Lists in Functions
* Passing a list directly gives the function mutable access to the original list object in memory.

```python
def print_models(unprinted_designs, completed_models):
    """Simulate printing each design until none are left."""
    while unprinted_designs:
        current_design = unprinted_designs.pop()
        print(f"Printing model: {current_design}")
        completed_models.append(current_design)

unprinted = ['iphone case', 'robot pendant', 'dodecahedron']
completed = []
print_models(unprinted, completed)
```

### 4.2 Preventing Modification with Slices (`[:]`)
* To preserve the original list contents, pass a shallow slice copy (`list_name[:]`) to the function call.

```python
print_models(unprinted[:], completed)
```

---

## 5. Passing an Arbitrary Number of Arguments

### 5.1 Arbitrary Positional Arguments (`*args`)
* An asterisk (`*`) preceding a parameter packs an arbitrary number of positional arguments into a **tuple**.

```python
def make_pizza(*toppings):
    """Summarize the pizza we are about to make."""
    print("\nMaking a pizza with the following toppings:")
    for topping in toppings:
        print(f"- {topping}")

make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
```

### 5.2 Mixing Positional and Arbitrary Arguments
* Parameters collecting arbitrary arguments must be placed **last** in the function definition header.

```python
def make_pizza(size, *toppings):
    """Summarize a pizza with a size and arbitrary toppings."""
    print(f"\nMaking a {size}-inch pizza with the following toppings:")
    for topping in toppings:
        print(f"- {topping}")

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```

### 5.3 Arbitrary Keyword Arguments (`**kwargs`)
* Double asterisks (`**`) pack an arbitrary number of name-value pairs into a **dictionary**.

```python
def build_profile(first, last, **user_info):
    """Build a dictionary containing everything known about a user."""
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    for key, value in user_info.items():
        profile[key] = value
    return profile

user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
print(user_profile)
```

---

## 6. Storing Functions in Modules

### 6.1 Importing Modules and Functions
* Separate functions into standalone `.py` module files to decouple implementation logic from executable driver scripts.

```python
# 1. Importing an entire module
import pizza
pizza.make_pizza(16, 'pepperoni')

# 2. Importing specific functions directly
from pizza import make_pizza
make_pizza(16, 'pepperoni')
```

### 6.2 Aliasing with `as`
* Use the `as` keyword to assign nicknames to imported functions or modules to prevent naming collisions and shorten call statements.

```python
# Aliasing a function
from pizza import make_pizza as mp
mp(16, 'pepperoni')

# Aliasing a module
import pizza as p
p.make_pizza(16, 'pepperoni')
```

### 6.3 Importing All Functions (`*`)
* `from module_name import *` imports every function into the global namespace.
* *Note: This is generally discouraged in large codebases due to namespace pollution and function overriding risks.*

---

## 7. Styling Functions (PEP 8)
* Use lowercase letters and underscores (`snake_case`) for function and module names.
* Every function must include a descriptive docstring immediately beneath the definition line.
* Do not use spaces around the `=` sign when specifying default parameter values or passing keyword arguments (`def func(param='default'):`).
* If a parameter list exceeds 79 characters, press Enter after the opening parenthesis and indent parameters with two tabs (8 spaces) to differentiate them from the function body.
* Separate individual function definitions with **two blank lines**.
* Place all `import` statements at the very top of the script file.

---

