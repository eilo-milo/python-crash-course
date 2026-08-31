
---

# Chapter 06: Dictionaries

---

## 1. What Is a Dictionary?

### 1.1 Structure and Syntax
* A dictionary is an unordered collection of key-value pairs wrapped in curly braces (`{}`)[cite: 5].
* Each key is connected to its value by a colon (`:`), and individual pairs are separated by commas[cite: 5].
* Keys can map to any Python object, including numbers, strings, lists, or other dictionaries[cite: 5].

```python
alien_0 = {'color': 'green', 'points': 5}
```

### 1.2 Accessing Values
* Values are retrieved by supplying the dictionary name followed by the desired key in square brackets: `dict_name[key]`[cite: 5].

```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0['color'])   # Output: green
print(alien_0['points'])  # Output: 5
```

### 1.3 Adding New Key-Value Pairs
* Dictionaries are dynamic structures; new pairs can be defined at any point during program execution[cite: 5].
* Key-value pairs can be added incrementally to an empty dictionary initialized as `{}`[cite: 5].

```python
alien_0 = {'color': 'green', 'points': 5}
alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)  # Output: {'color': 'green', 'points': 5, 'y_position': 25, 'x_position': 0}
```

### 1.4 Modifying Values
* Reassigning a value is performed by referencing an existing key and assigning a new value[cite: 5].

```python
alien_0 = {'color': 'green', 'speed': 'medium', 'x_position': 0}

# Move alien to the right depending on its speed
if alien_0['speed'] == 'slow':
    x_increment = 1
elif alien_0['speed'] == 'medium':
    x_increment = 2
else:
    x_increment = 3

alien_0['x_position'] = alien_0['x_position'] + x_increment
```

### 1.5 Removing Key-Value Pairs with `del`
* The `del` statement permanently deletes a specific key-value pair from memory[cite: 5].

```python
alien_0 = {'color': 'green', 'points': 5}
del alien_0['points']
print(alien_0)  # Output: {'color': 'green'}
```

### 1.6 Structuring Dictionaries of Similar Objects
* Dictionaries can store one kind of attribute for many independent objects, formatted with multi-line indentation for readability[cite: 5].

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}
```

---

## 2. Looping Through a Dictionary

### 2.1 Looping Through Key-Value Pairs (`.items()`)
* The `.items()` method returns an iterable sequence of key-value tuples, unpacked into two distinct loop variables[cite: 5].

```python
user_0 = {
    'username': 'efermi',
    'first': 'enrico',
    'last': 'fermi',
}

for key, value in user_0.items():
    print(f"\nKey: {key}")
    print(f"Value: {value}")
```

### 2.2 Looping Through Keys (`.keys()`)
* The `.keys()` method returns an iterable sequence containing only the dictionary keys[cite: 5].
* Iterating over keys is the default behavior when looping directly through a dictionary object (`for name in dict:` is equivalent to `for name in dict.keys():`)[cite: 5].

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

for name in favorite_languages.keys():
    print(name.title())
```

### 2.3 Looping Through Keys in Sorted Order
* Wrapping `sorted()` around `.keys()` orders the dictionary keys alphabetically for display without modifying the dictionary itself[cite: 5].

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

for name in sorted(favorite_languages.keys()):
    print(name.title() + ", thank you for taking the poll.")
```

### 2.4 Looping Through Values (`.values()`) and Sets
* The `.values()` method retrieves values without their corresponding keys, which may include duplicate entries[cite: 5].
* Wrapping `set()` around `.values()` discards duplicate elements, leaving only unique values[cite: 5].

```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
}

for language in set(favorite_languages.values()):
    print(language.title())
```

---

## 3. Nesting Data Structures

### 3.1 A List of Dictionaries
* Groups multiple dictionaries representing distinct entities inside a single list[cite: 5].
* Allows dynamic batch generation and element modification using loops[cite: 5].

```python
# Create a fleet of 30 green aliens
aliens = []
for alien_number in range(30):
    new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
    aliens.append(new_alien)

# Modify the first 3 aliens
for alien in aliens[:3]:
    if alien['color'] == 'green':
        alien['color'] = 'yellow'
        alien['speed'] = 'medium'
        alien['points'] = 10
```

### 3.2 A List Inside a Dictionary
* Enables associating multiple values with a single descriptive key[cite: 5].

```python
pizza = {
    'crust': 'thick',
    'toppings': ['mushrooms', 'extra cheese'],
}

print("You ordered a " + pizza['crust'] + "-crust pizza with:")
for topping in pizza['toppings']:
    print("\t" + topping)
```

### 3.3 A Dictionary Inside a Dictionary
* Maps unique parent keys (such as usernames) to inner dictionary records containing specific attributes[cite: 5].

```python
users = {
    'aeinstein': {
        'first': 'albert',
        'last': 'einstein',
        'location': 'princeton',
    },
    'mcurie': {
        'first': 'marie',
        'last': 'curie',
        'location': 'paris',
    },
}

for username, user_info in users.items():
    print(f"\nUsername: {username}")
    print(f"\tFull name: {user_info['first'].title()} {user_info['last'].title()}")
    print(f"\tLocation: {user_info['location'].title()}")
```

---
