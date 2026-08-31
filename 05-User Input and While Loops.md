
---

# Chapter 07: User Input and While Loops

---

## 1. How the `input()` Function Works
* The `input()` function pauses program execution, displays a prompt to the terminal, and waits for user input.
* Once the user submits input (by pressing Enter), Python captures the response and stores it as a string in a variable.

```python
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```

### 1.1 Writing Clear and Multi-line Prompts
* Prompts should include a trailing space after delimiters (such as colons or question marks) to separate the prompt text visually from user input.
* For longer instructions, multi-line prompt strings can be constructed incrementally using the `+=` string operator and passed directly into `input()`.

```python
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "

name = input(prompt)
print(f"\nHello, {name}!")
```

### 1.2 Converting String Input with `int()`
* The `input()` function treats all captured input strictly as string (`str`) data.
* Directly performing mathematical comparisons on raw string input results in a `TypeError: unorderable types: str() >= int()`.
* Wrap string representations in `int()` to convert them explicitly into numerical values before calculation or comparison.

```python
height = input("How tall are you, in inches? ")
height = int(height)

if height >= 36:
    print("\nYou're tall enough to ride!")
else:
    print("\nYou'll be able to ride when you're a little older.")
```

### 1.3 The Modulo Operator (`%`)
* Divides one number by another and returns the remainder (e.g., `7 % 3` yields `1`).
* Frequently used to determine parity: if `number % 2 == 0`, the number is even; otherwise, it is odd.

```python
number = input("Enter a number, and I'll tell you if it's even or odd: ")
number = int(number)

if number % 2 == 0:
    print(f"\nThe number {number} is even.")
else:
    print(f"\nThe number {number} is odd.")
```

### 1.4 Python 2.7 Differences (`raw_input`)
* In Python 2.7, `raw_input()` must be used to collect input as a string.
* The legacy `input()` in Python 2 attempts to evaluate user input as executable Python code, which presents errors and security risks.

---

## 2. Introducing `while` Loops

### 2.1 The `while` Loop in Action
* Unlike `for` loops that iterate over fixed collections once per element, a `while` loop executes continuously as long as a specified condition evaluates to `True`.

```python
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1
```

### 2.2 Letting the User Choose When to Quit
* A sentinel value (such as `'quit'`) can control loop termination by comparing input directly in the `while` conditional statement.

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
    message = input(prompt)
    if message != 'quit':
        print(message)
```

### 2.3 Using a Flag
* A **flag** is a Boolean variable that dictates whether the overall program loop continues executing.
* Centralizing execution status in a single flag keeps `while` headers clean when multiple complex events or conditions can trigger program shutdown.

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
    message = input(prompt)
    if message == 'quit':
        active = False
    else:
        print(message)
```

### 2.4 Using `break` to Exit a Loop
* The `break` statement immediately terminates loop execution, bypassing any remaining instructions in the block and exiting to code following the loop.
* `break` can be used to control loops initialized with infinite conditions like `while True:`.

```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "

while True:
    city = input(prompt)
    if city == 'quit':
        break
    else:
        print(f"I'd love to go to {city.title()}!")
```

### 2.5 Using `continue` in a Loop
* The `continue` statement skips the rest of the current iteration and returns program execution immediately to the beginning of the loop condition.

```python
current_number = 0
while current_number < 10:
    current_number += 1
    if current_number % 2 == 0:
        continue
    print(current_number)  # Prints only odd numbers: 1, 3, 5, 7, 9
```

### 2.6 Avoiding Infinite Loops
* A `while` loop becomes infinite if its conditional test never evaluates to `False` or if it cannot reach a `break` statement (such as forgetting to increment a counter variable).
* To break out of an infinite loop in a terminal session, press `CTRL-C` or terminate the running terminal process.

---

## 3. Using `while` Loops with Lists and Dictionaries

### 3.1 Moving Items Between Lists
* Mutating a list while iterating over it with a `for` loop causes internal tracking errors; dynamic list modifications during iteration require a `while` loop.
* Using `while list_name:` evaluates to `True` until the list is empty, allowing items to be popped and moved sequentially.

```python
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print(f"Verifying user: {current_user.title()}")
    confirmed_users.append(current_user)

print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())
```

### 3.2 Removing All Instances of a Value from a List
* The standard `.remove()` method eliminates only the first matching occurrence of a value.
* Running `.remove()` inside a `while value in list:` loop purges all instances of a target element from the list.

```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']

while 'cat' in pets:
    pets.remove('cat')

print(pets)  # Output: ['dog', 'dog', 'goldfish', 'rabbit']
```

### 3.3 Filling a Dictionary with User Input
* Repeated prompts can populate key-value pairs in a dictionary dynamically with each iteration through a `while` loop.

```python
responses = {}
polling_active = True

while polling_active:
    name = input("\nWhat is your name? ")
    response = input("Which mountain would you like to climb someday? ")
    
    responses[name] = response
    
    repeat = input("Would you like to let another person respond? (yes/ no) ")
    if repeat.lower() == 'no':
        polling_active = False

print("\n--- Poll Results ---")
for name, response in responses.items():
    print(f"{name} would like to climb {response}.")
```

---
