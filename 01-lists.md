
---

# Chapter 03: Introducing Lists

---

## 1. What Is a List?
* A list is an ordered collection of items enclosed in square brackets (`[...]`), with elements separated by commas.
* Lists can contain any combination of data types (numbers, strings, etc.) and do not require elements to be related.
* By convention, list variable names should be plural (e.g., `letters`, `digits`, `names`).
* Printing a list directly outputs its internal representation, including brackets and quotation marks.

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)  # Output: ['trek', 'cannondale', 'redline', 'specialized']
```

---

## 2. Accessing Elements in a List

### 2.1 Zero-Based Indexing
* Elements in a list are accessed by specifying their index within square brackets: `list_name[index]`.
* Python uses zero-based indexing; the first element is at index `0`, the second at `1`, and the $n$-th element at index $n - 1$.
* Accessing a single element returns the raw value without quotes or brackets, allowing string formatting methods (such as `.title()`) to be applied directly.

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0])          # Output: trek
print(bicycles[0].title())  # Output: Trek
```

### 2.2 Negative Indexing
* Index `-1` accesses the last element of a list without requiring knowledge of its total length.
* Negative indexing continues backward: `-2` returns the second to last item, `-3` returns the third to last, and so on.

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[-1])  # Output: specialized
print(bicycles[-2])  # Output: redline
```

### 2.3 Using Individual List Values
* Values retrieved by index can be stored in variables or concatenated into formatted string messages.

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
message = "My first bicycle was a " + bicycles[0].title() + "."
print(message)  # Output: My first bicycle was a Trek.
```

---

## 3. Changing, Adding, and Removing Elements

### 3.1 Modifying Elements
* An existing element can be modified by assigning a new value to its specific index.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles[0] = 'ducati'
print(motorcycles)  # Output: ['ducati', 'yamaha', 'suzuki']
```

### 3.2 Adding Elements (`append` & `insert`)
* **`append(value)`**: Adds a new item to the end of the list without modifying existing elements; standard for dynamically building lists starting from an empty list `[]`.
* **`insert(index, value)`**: Inserts a new element at a specified index, shifting all subsequent elements one position to the right.

```python
motorcycles = []
motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.insert(0, 'ducati')
print(motorcycles)  # Output: ['ducati', 'honda', 'yamaha']
```

### 3.3 Removing Elements (`del`, `pop`, & `remove`)
* **`del list[index]`**: Deletes the item at the specified index permanently when the deleted value is no longer needed.
* **`pop(index=-1)`**: Removes and returns an item from the list (defaults to the last item if no index is passed), useful for stack-like operations or when the removed value must be preserved in a variable.
* **`remove(value)`**: Deletes an item by value when its index is unknown; deletes only the **first occurrence** of that value.

```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']

# Deleting by position
del motorcycles[0]       # Removes 'honda'

# Popping by position (or default end)
popped_bike = motorcycles.pop()  # Removes and returns 'ducati'

# Removing by value
too_expensive = 'yamaha'
motorcycles.remove(too_expensive)
```

---

## 4. Organizing a List

### 4.1 Permanent Sorting with `sort()`
* `.sort()`: Alphabetically sorts a list permanently in place.
* `.sort(reverse=True)`: Permanently sorts the list in reverse alphabetical order.

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()
print(cars)  # Output: ['audi', 'bmw', 'subaru', 'toyota']

cars.sort(reverse=True)
print(cars)  # Output: ['toyota', 'subaru', 'bmw', 'audi']
```

### 4.2 Temporary Sorting with `sorted()`
* `sorted(list)`: Returns a new, sorted copy of the list while leaving the original list unaltered.
* Can also accept the optional argument `reverse=True`.

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(sorted(cars))  # Output: ['audi', 'bmw', 'subaru', 'toyota']
print(cars)          # Output: ['bmw', 'audi', 'toyota', 'subaru']
```

### 4.3 Reversing List Order with `reverse()`
* `.reverse()`: Permanently reverses the current order of the elements in place (it does not sort alphabetically in reverse).
* Applying `.reverse()` a second time restores the original order.

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.reverse()
print(cars)  # Output: ['subaru', 'toyota', 'audi', 'bmw']
```

### 4.4 Finding Length with `len()`
* `len(list)`: Returns the total count of elements in the list, counting from `1` (not zero-indexed).

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars))  # Output: 4
```

---

## 5. Avoiding Index Errors
* An `IndexError: list index out of range` occurs when requesting an index that does not exist (commonly caused by off-by-one counting errors).
* `list[-1]` consistently accesses the last element, but requesting `[-1]` on an empty list (`[]`) causes an `IndexError`.
* When debugging index errors, printing the list or checking its length via `len(list)` helps verify dynamic runtime state.

---

<!-- Navigation Footer -->
[← Previous Chapter](chapter-02.md) | [Table of Contents](../README.md) | [Next Chapter →](chapter-04.md)
