
---

# Chapter 05: If Statements

---

## 1. Conditional Tests
* A conditional test is an expression that evaluates strictly to a Boolean value (`True` or `False`)[cite: 4].
* Python uses these Boolean evaluations to determine whether the code block associated with an `if` branch executes[cite: 4].

### 1.1 Equality and Case Sensitivity
* Equality is tested using the double equal sign (`==`), whereas a single equal sign (`=`) is used for variable assignment[cite: 4].
* String equality checks are case sensitive in Python (`'Audi' == 'audi'` evaluates to `False`)[cite: 4].
* To implement case-insensitive comparisons without mutating original variables, apply `.lower()` during evaluation[cite: 4].

```python
car = 'Audi'
print(car.lower() == 'audi')  # True
print(car)                    # 'Audi' (unmodified)
```


### 1.2 Inequality
* The inequality operator (`!=`) evaluates to `True` if the compared operands do not match[cite: 4].

```python
requested_topping = 'mushrooms'
if requested_topping != 'anchovies':
    print("Hold the anchovies!")
```


### 1.3 Numerical Comparisons
* Supported comparison operators include: `==`, `!=`, `<`, `<=`, `>`, and `>=`[cite: 4].

```python
age = 19
print(age < 21)   # True
print(age >= 21)  # False
```


### 1.4 Checking Multiple Conditions (`and` / `or`)
* **`and`**: Returns `True` only if **all** individual sub-conditions evaluate to `True`[cite: 4].
* **`or`**: Returns `True` if **at least one** sub-condition evaluates to `True`; returns `False` only when all sub-conditions fail[cite: 4].

```python
age_0 = 22
age_1 = 18

print((age_0 >= 21) and (age_1 >= 21))  # False
print((age_0 >= 21) or (age_1 >= 21))   # True
```

### 1.5 Checking List Membership (`in` / `not in`)
* **`in`**: Checks whether a specified value is present within a collection[cite: 4].
* **`not in`**: Checks whether a specified value does not appear in a collection[cite: 4].

```python
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'

if user not in banned_users:
    print(user.title() + ", you can post a response if you wish.")
```


### 1.6 Boolean Expressions
* A Boolean value is either `True` or `False`[cite: 4].
* Frequently utilized as flags to monitor runtime states (e.g., `game_active = True`, `can_edit = False`)[cite: 4].

---

## 2. The `if` Statement Syntax

### 2.1 Simple `if` Statements
* Consists of a single conditional test and an indented block executed only when the test evaluates to `True`[cite: 4].

```python
age = 19
if age >= 18:
    print("You are old enough to vote!")
```


### 2.2 The `if-else` Chain
* Provides two distinct execution paths: the `if` block executes when the condition passes, and the `else` block executes for all failing conditions[cite: 4].

```python
age = 17
if age >= 18:
    print("You are old enough to vote!")
else:
    print("Sorry, you are too young to vote.")
```


### 2.3 The `if-elif-else` Chain
* Evaluates multiple conditions sequentially until one passes; once a test passes, its block executes and Python skips all remaining branches[cite: 4].
* Setting values inside branches and utilizing a single output call after the chain improves code maintainability[cite: 4].

```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10

print("Your admission cost is $" + str(price) + ".")
```


### 2.4 Multiple `elif` Blocks & Omitting `else`
* Multiple `elif` blocks can be chained to handle granular criteria[cite: 4].
* The `else` block is optional[cite: 4]. A terminating `elif` block can replace a generic `else` to prevent unintended catchall execution on unexpected data[cite: 4].

```python
age = 65

if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
elif age >= 65:
    price = 5
```


### 2.5 Testing Multiple Independent Conditions
* When multiple conditions must be evaluated and acted upon simultaneously, use independent `if` statements instead of `elif` or `else` constructs[cite: 4].

```python
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
    print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
    print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")
```


---

## 3. Using `if` Statements with Lists

### 3.1 Checking for Special Items
* Conditional tests placed inside `for` loops allow selective handling of specific elements while processing the list[cite: 4].

```python
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")
    else:
        print("Adding " + requested_topping + ".")
```

### 3.2 Checking That a List Is Not Empty
* Passing a list name directly as a conditional test (`if requested_toppings:`) returns `True` if it contains items and `False` if it is empty (`[]`)[cite: 4].

```python
requested_toppings = []

if requested_toppings:
    for requested_topping in requested_toppings:
        print("Adding " + requested_topping + ".")
else:
    print("Are you sure you want a plain pizza?")
```


### 3.3 Working with Multiple Lists
* Elements from an input list can be cross-checked against a master lookup list (or tuple) using the `in` keyword inside a loop[cite: 4].

```python
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print("Adding " + requested_topping + ".")
    else:
        print("Sorry, we don't have " + requested_topping + ".")
```


---

## 4. Styling Conditional Tests (PEP 8)
* PEP 8 recommends placing a single space around all comparison operators (`==`, `!=`, `<`, `>`, `<=`, `>=`)[cite: 4].
* Example: `if age < 4:` is preferred over `if age<4:`[cite: 4].

---
