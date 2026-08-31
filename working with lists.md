
---

# Chapter 04: Working with Lists

---

## 1. Looping Through an Entire List

### 1.1 The `for` Loop Mechanism
* A `for` loop automates repetitive tasks by iterating through every element in a sequence.
* Python assigns each element in sequence to a temporary loop variable, executing the indented block once per item.
* Standard convention uses singular names for the iteration variable and plural names for the collection (e.g., `for cat in cats:`).

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician)
```

### 1.2 Doing Work Inside and After Loops
* Multiple indented statements execute sequentially on each pass through the loop.
* Any unindented code following the loop block executes only once after the entire loop finishes iterating.

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("I can't wait to see your next trick, " + magician.title() + ".\n")

print("Thank you, everyone. That was a great magic show!")
```

---

## 2. Avoiding Indentation Errors
* **Forgetting to indent**: Omitting indentation on the line directly beneath a `for` statement triggers an `IndentationError: expected an indented block`.
* **Forgetting to indent additional lines**: Leads to logical errors where only the first indented line repeats per item, while following unindented lines run once using the loop variable's final value.
* **Indenting unnecessarily**: Adding indentation to standard sequential code causes an `IndentationError: unexpected indent`.
* **Indenting unnecessarily after the loop**: Causes code intended to run once at the conclusion to repeat on every iteration.
* **Forgetting the colon (`:`)**: Omitting the colon at the end of the loop header statement raises a `SyntaxError`.

---

## 3. Making Numerical Lists

### 3.1 The `range()` Function
* Generates a sequence of integers starting at the first argument and stopping one unit before the second argument (off-by-one behavior).
* `range(1, 5)` generates `1, 2, 3, 4`.
* A third argument specifies step size: `range(2, 11, 2)` generates even numbers `[2, 4, 6, 8, 10]`.

### 3.2 Using `range()` to Make a List
* Passing a `range()` object into the `list()` constructor directly converts the numerical sequence into a Python list.

```python
numbers = list(range(1, 6))
print(numbers)  # Output: [1, 2, 3, 4, 5]

squares = []
for value in range(1, 11):
    squares.append(value ** 2)
print(squares)  # Output: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### 3.3 Simple Statistics with Numerical Lists
* Built-in statistical helper functions operate directly on numeric collections:
  * `min(list)`: Returns the smallest number.
  * `max(list)`: Returns the largest number.
  * `sum(list)`: Returns the total sum of all elements.

```python
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(min(digits))  # Output: 0
print(max(digits))  # Output: 9
print(sum(digits))  # Output: 45
```

### 3.4 List Comprehensions
* Combines loop generation and element creation into a single concise line inside square brackets.
* General syntax: `[expression for item in iterable]`.

```python
squares = [value ** 2 for value in range(1, 11)]
print(squares)  # Output: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

---

## 4. Working with Part of a List

### 4.1 Slicing a List
* Uses colon notation inside square brackets `list[start:stop]` (includes `start`, excludes `stop`).
* Omitting the start index (`[:4]`) automatically begins the slice at index `0`.
* Omitting the stop index (`[2:]`) slices through the remainder of the list.
* Negative start indices slice relative to the end (e.g., `[-3:]` extracts the final three items).

```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3])  # Output: ['charles', 'martina', 'michael']
print(players[:4])   # Output: ['charles', 'martina', 'michael', 'florence']
print(players[2:])   # Output: ['michael', 'florence', 'eli']
print(players[-3:])  # Output: ['michael', 'florence', 'eli']
```

### 4.2 Looping Through a Slice
* A slice can serve directly as the iterable in a `for` loop to process a subset of elements.

```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
for player in players[:3]:
    print(player.title())
```

### 4.3 Copying a List Properly
* **Correct Copying**: Slicing the entire list `[:]` generates an independent duplicate copy.
* **Incorrect Copying**: Direct assignment (`list_b = list_a`) binds both variables to the exact same list in memory, causing mutations in one to reflect in the other.

```python
my_foods = ['pizza', 'falafel', 'carrot cake']

# Independent copy using a slice
friend_foods = my_foods[:]
my_foods.append('cannoli')
friend_foods.append('ice cream')

print(my_foods)      # ['pizza', 'falafel', 'carrot cake', 'cannoli']
print(friend_foods)  # ['pizza', 'falafel', 'carrot cake', 'ice cream']
```

---

## 5. Tuples

### 5.1 Defining and Accessing Tuples
* A tuple is an **immutable** sequence defined using parentheses (`(...)`) instead of square brackets.
* Elements are accessed using standard zero-based indexing syntax `tuple[index]`.

```python
dimensions = (200, 50)
print(dimensions[0])  # Output: 200
print(dimensions[1])  # Output: 50
```

### 5.2 Immutability and Overwriting Tuples
* Direct item reassignment (e.g., `dimensions[0] = 250`) is rejected with a `TypeError: 'tuple' object does not support item assignment`.
* To alter values associated with a tuple variable, the entire tuple must be reassigned/overwritten.

```python
dimensions = (200, 50)
# Overwriting the variable with a new tuple object
dimensions = (400, 100)
```

---

## 6. Styling Your Code (PEP 8)
* **Indentation**: Use exactly **4 spaces** per indentation level. Configure text editors to convert tab key presses into 4 spaces.
* **Line Length**: Keep lines under **79 characters** for code logic and under **72 characters** for docstrings/comments.
* **Blank Lines**: Use single blank lines purposefully to separate logical sections without excessive vertical spacing.

---
