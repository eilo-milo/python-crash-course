# Chapter 02: Variables and Simple Data Types

---

## 1. Program Execution & Syntax Highlighting
* The `.py` file extension identifies the file as a Python script.
* The Python interpreter executes code line by line, evaluating functions and keywords (e.g., `print()` outputs data to the terminal).
* Code editors use **syntax highlighting** to distinguish language keywords, variables, and literal values using different colors.

---

## 2. Variables
* A variable is a named storage reference that holds a specific value in memory.
* Values can be dynamically updated throughout the lifecycle of a script.

```python
message = "Hello Python world!"
print(message)

message = "Hello Python Crash Course world!"
print(message)
```

### 2.1 Naming Rules and Conventions
* Allowed characters: Letters, numbers, and underscores (`_`).
* Numbers cannot start a variable name (`message_1` is valid; `1_message` is invalid).
* Spaces are strictly disallowed; use snake_case (`student_name`).
* Avoid using reserved Python keywords (e.g., `print`, `for`, `if`, `class`).
* Use lowercase names by convention, and avoid confusing single characters like lowercase `l` and uppercase `O`.

### 2.2 Name Errors and Tracebacks
* A `NameError` occurs when referencing an identifier that has not been defined or contains a typo.
* Python provides a **traceback** indicating the file name, line number, and error type.

```python
message = "Hello Python Crash Course reader!"
# Causes NameError: name 'mesage' is not defined
print(mesage)
```

---

## 3. Strings

### 3.1 Definition and Quotes
* A string is a sequence of characters enclosed in either single (`'...'`) or double (`"..."`) quotes.
* Mixing quote types allows effortless inclusion of quotes and apostrophes inside strings.

```python
quote = 'Albert Einstein once said, "A person who never made a mistake never tried anything new."'
sentence = "One of Python's strengths is its diverse community."
```

### 3.2 Changing Case with Methods
* `.title()`: Converts each word to titlecase (capitalizes the first letter).
* `.upper()`: Converts all characters to uppercase.
* `.lower()`: Converts all characters to lowercase (ideal for standardizing input data before persistence).

```python
name = "ada lovelace"
print(name.title())  # Output: Ada Lovelace
print(name.upper())  # Output: ADA LOVELACE
print(name.lower())  # Output: ada lovelace
```

### 3.3 String Concatenation
* Strings can be merged using the addition operator (`+`).

```python
first_name = "ada"
last_name = "lovelace"
full_name = first_name + " " + last_name
message = "Hello, " + full_name.title() + "!"
print(message)  # Output: Hello, Ada Lovelace!
```

### 3.4 Whitespace, Tabs, and Newlines
* `\t`: Adds a tab space.
* `\n`: Inserts a line break.

```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
```

### 3.5 Stripping Whitespace
* Whitespace modifications return a new string and do not mutate in place unless reassigned.
* `.rstrip()`: Strips trailing (right) whitespace.
* `.lstrip()`: Strips leading (left) whitespace.
* `.strip()`: Strips whitespace from both ends.

```python
favorite_language = " python "
favorite_language = favorite_language.strip()
print(favorite_language)  # Output: 'python'
```

### 3.6 Avoiding Syntax Errors
* Unmatched quotes cause a `SyntaxError`. Always enclose strings containing single quote apostrophes inside double quotes, or escape them.

```python
# Valid:
valid_msg = "It's a sunny day."

# Invalid (Throws SyntaxError):
# invalid_msg = 'It's a sunny day.'
```

---

## 4. Numbers

### 4.1 Integers
* Supports standard arithmetic: `+`, `-`, `*`, `/`.
* Exponentiation uses `**` (e.g., `3 ** 2` results in `9`).
* Standard PEMDAS order of operations is respected; use parentheses `()` to enforce evaluation order.

### 4.2 Floats
* Any number containing a decimal point is treated as a float.
* Due to computer binary representation constraints, float arithmetic can produce long fractional representations (e.g., `0.2 + 0.1` produces `0.30000000000000004`).

### 4.3 Type Conversion with `str()`
* Direct concatenation between strings and integer types triggers a `TypeError`.
* Wrap numeric variables in `str()` to convert them explicitly to string objects.

```python
age = 23
message = "Happy " + str(age) + "rd Birthday!"
print(message)
```

### 4.4 Python 2 vs. Python 3 Division
* **Python 3**: `3 / 2` evaluates to float `1.5`.
* **Python 2**: `3 / 2` performs integer floor division returning `1` (requires float operand like `3.0 / 2` to obtain `1.5`).

---

## 5. Comments
* Use the hash symbol (`#`) for single-line comments.
* Comments clarify program architecture, explain algorithmic decisions, and improve maintainability for collaborative development.

```python
# Calculate user age and format greeting
user_age = 25
```

---

## 6. The Zen of Python
Access principles via the Python interpreter using `import this`.

* **Beautiful is better than ugly**: Strive for clean, aesthetic structure.
* **Simple is better than complex**: Choose direct solutions over over-engineered ones.
* **Complex is better than complicated**: When complexity is required, keep the design modular and clear.
* **Readability counts**: Write code meant to be read by humans.
* **There should be one—and preferably only one—obvious way to do it**: Standard conventions make collaboration predictable.
* **Now is better than never**: Write working code first, then iterate.
