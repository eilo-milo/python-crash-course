# Chapter 02: Variables and Simple Data Types

## Table of Contents
- [1. Program Execution & Syntax Highlighting](#1-program-execution--syntax-highlighting)
- [2. Variables](#2-variables)
  - [2.1 Naming Rules and Conventions](#21-naming-rules-and-conventions)
  - [2.2 Name Errors and Tracebacks](#22-name-errors-and-tracebacks)
- [3. Strings](#3-strings)
  - [3.1 Definition and Quotes](#31-definition-and-quotes)
  - [3.2 Changing Case with Methods](#32-changing-case-with-methods)
  - [3.3 String Concatenation](#33-string-concatenation)
  - [3.4 Whitespace, Tabs, and Newlines](#34-whitespace-tabs-and-newlines)
  - [3.5 Stripping Whitespace](#35-stripping-whitespace)
  - [3.6 Avoiding Syntax Errors](#36-avoiding-syntax-errors)
- [4. Numbers](#4-numbers)
  - [4.1 Integers](#41-integers)
  - [4.2 Floats](#42-floats)
  - [4.3 Type Conversion with `str()`](#43-type-conversion-with-str)
  - [4.4 Python 2 vs. Python 3 Division](#44-python-2-vs-python-3-division)
- [5. Comments](#5-comments)
- [6. The Zen of Python](#6-the-zen-of-python)

---

## 1. Program Execution & Syntax Highlighting
* The `.py` file extension identifies the file as a Python script[cite: 1].
* The Python interpreter executes code line by line, evaluating functions and keywords (e.g., `print()` outputs data to the terminal)[cite: 1].
* Code editors use **syntax highlighting** to distinguish language keywords, variables, and literal values using different colors[cite: 1].

---

## 2. Variables
* A variable is a named storage reference that holds a specific value in memory[cite: 1].
* Values can be dynamically updated throughout the lifecycle of a script[cite: 1].

```python
message = "Hello Python world!"
print(message)

message = "Hello Python Crash Course world!"
print(message)
```

### 2.1 Naming Rules and Conventions
* Allowed characters: Letters, numbers, and underscores (`_`)[cite: 1].
* Numbers cannot start a variable name (`message_1` is valid; `1_message` is invalid)[cite: 1].
* Spaces are strictly disallowed; use snake_case (`student_name`)[cite: 1].
* Avoid using reserved Python keywords (e.g., `print`, `for`, `if`, `class`)[cite: 1].
* Use lowercase names by convention, and avoid confusing single characters like lowercase `l` and uppercase `O`[cite: 1].

### 2.2 Name Errors and Tracebacks
* A `NameError` occurs when referencing an identifier that has not been defined or contains a typo[cite: 1].
* Python provides a **traceback** indicating the file name, line number, and error type[cite: 1].

```python
message = "Hello Python Crash Course reader!"
# Causes NameError: name 'mesage' is not defined
print(mesage)
```

---

## 3. Strings

### 3.1 Definition and Quotes
* A string is a sequence of characters enclosed in either single (`'...'`) or double (`"..."`) quotes[cite: 1].
* Mixing quote types allows effortless inclusion of quotes and apostrophes inside strings[cite: 1].

```python
quote = 'Albert Einstein once said, "A person who never made a mistake never tried anything new."'
sentence = "One of Python's strengths is its diverse community."
```

### 3.2 Changing Case with Methods
* `.title()`: Converts each word to titlecase (capitalizes the first letter)[cite: 1].
* `.upper()`: Converts all characters to uppercase[cite: 1].
* `.lower()`: Converts all characters to lowercase (ideal for standardizing input data before persistence)[cite: 1].

```python
name = "ada lovelace"
print(name.title())  # Output: Ada Lovelace
print(name.upper())  # Output: ADA LOVELACE
print(name.lower())  # Output: ada lovelace
```

### 3.3 String Concatenation
* Strings can be merged using the addition operator (`+`)[cite: 1].

```python
first_name = "ada"
last_name = "lovelace"
full_name = first_name + " " + last_name
message = "Hello, " + full_name.title() + "!"
print(message)  # Output: Hello, Ada Lovelace!
```

### 3.4 Whitespace, Tabs, and Newlines
* `\t`: Adds a tab space[cite: 1].
* `\n`: Inserts a line break[cite: 1].

```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
```

### 3.5 Stripping Whitespace
* Whitespace modifications return a new string and do not mutate in place unless reassigned[cite: 1].
* `.rstrip()`: Strips trailing (right) whitespace[cite: 1].
* `.lstrip()`: Strips leading (left) whitespace[cite: 1].
* `.strip()`: Strips whitespace from both ends[cite: 1].

```python
favorite_language = " python "
favorite_language = favorite_language.strip()
print(favorite_language)  # Output: 'python'
```

### 3.6 Avoiding Syntax Errors
* Unmatched quotes cause a `SyntaxError`[cite: 1]. Always enclose strings containing single quote apostrophes inside double quotes, or escape them[cite: 1].

```python
# Valid:
valid_msg = "It's a sunny day."

# Invalid (Throws SyntaxError):
# invalid_msg = 'It's a sunny day.'
```

---

## 4. Numbers

### 4.1 Integers
* Supports standard arithmetic: `+`, `-`, `*`, `/`[cite: 1].
* Exponentiation uses `**` (e.g., `3 ** 2` results in `9`)[cite: 1].
* Standard PEMDAS order of operations is respected; use parentheses `()` to enforce evaluation order[cite: 1].

### 4.2 Floats
* Any number containing a decimal point is treated as a float[cite: 1].
* Due to computer binary representation constraints, float arithmetic can produce long fractional representations (e.g., `0.2 + 0.1` produces `0.30000000000000004`)[cite: 1].

### 4.3 Type Conversion with `str()`
* Direct concatenation between strings and integer types triggers a `TypeError`[cite: 1].
* Wrap numeric variables in `str()` to convert them explicitly to string objects[cite: 1].

```python
age = 23
message = "Happy " + str(age) + "rd Birthday!"
print(message)
```

### 4.4 Python 2 vs. Python 3 Division
* **Python 3**: `3 / 2` evaluates to float `1.5`[cite: 1].
* **Python 2**: `3 / 2` performs integer floor division returning `1` (requires float operand like `3.0 / 2` to obtain `1.5`)[cite: 1].

---

## 5. Comments
* Use the hash symbol (`#`) for single-line comments[cite: 1].
* Comments clarify program architecture, explain algorithmic decisions, and improve maintainability for collaborative development[cite: 1].

```python
# Calculate user age and format greeting
user_age = 25
```

---

## 6. The Zen of Python
Access principles via the Python interpreter using `import this`[cite: 1].

* **Beautiful is better than ugly**: Strive for clean, aesthetic structure[cite: 1].
* **Simple is better than complex**: Choose direct solutions over over-engineered ones[cite: 1].
* **Complex is better than complicated**: When complexity is required, keep the design modular and clear[cite: 1].
* **Readability counts**: Write code meant to be read by humans[cite: 1].
* **There should be one—and preferably only one—obvious way to do it**: Standard conventions make collaboration predictable[cite: 1].
* **Now is better than never**: Write working code first, then iterate[cite: 1].
