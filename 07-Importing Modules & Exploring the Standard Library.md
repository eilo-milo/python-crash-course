

---

# Importing Modules & Exploring the Standard Library

---

## 1. Module Import Fundamentals

### 1.1 How Imports Execute Code
* When a module is imported, Python runs **all** top-level statements inside that file immediately, defining its functions, classes, and variables.
* Any top-level executable code (such as `print()` statements) will run at the moment of import.

```python
# my_module.py
print("Importing my_module...")

test = "Test String"

def find_index(to_search, target):
    """Find the index of a value in a sequence."""
    for i, value in enumerate(to_search):
        if value == target:
            return i
    return -1
```

### 1.2 Import Syntax Variations

#### 1. Importing the Full Module
* Requires dot notation to access attributes and functions.

```python
import my_module

courses = ['History', 'Math', 'Physics', 'CompSci']
index = my_module.find_index(courses, 'Math')
print(index)  # Output: 1
```

#### 2. Aliasing a Module (`as`)
* Shortens module references to improve conciseness (standard convention with libraries like `numpy as np` or `pandas as pd`).

```python
import my_module as mm

index = mm.find_index(courses, 'Math')
```

#### 3. Importing Specific Members Directly (`from ... import ...`)
* Brings specific functions or variables directly into the current namespace, removing the need for module prefixes.
* Does not import unlisted members (e.g., `test` is not accessible unless explicitly listed).

```python
from my_module import find_index, test

index = find_index(courses, 'Math')
print(test)
```

#### 4. Aliasing Specific Functions
* Allows renaming imported items directly inside the script.

```python
from my_module import find_index as fi

index = fi(courses, 'Math')
```

### 1.3 The Asterisk (`*`) Import Caveat
* `from module_name import *` imports every attribute and function into the local namespace.
* **Why it is discouraged**: It obscures where functions/variables were defined and risks silent name collisions (overwriting local variables or functions).

---

## 2. How Python Finds Modules (`sys.path`)

### 2.1 Search Priority Order
Python locates modules by sequentially traversing directory paths stored in `sys.path`:

1. **Current Directory**: The folder containing the script currently being run.
2. **`PYTHONPATH`**: Directories listed in the operating system's `PYTHONPATH` environment variable.
3. **Standard Library**: Built-in Python library directories.
4. **Site-Packages**: Third-party packages installed via package managers like `pip`.

```python
import sys
print(sys.path)
```

### 2.2 Modifying `sys.path` Programmatically
* Because `sys.path` is a standard Python list, custom search paths can be appended dynamically at runtime before running imports.

```python
import sys
sys.path.append('/path/to/custom/modules')

import my_module
```

### 2.3 Configuring the `PYTHONPATH` Environment Variable
Adding custom module directories permanently to `PYTHONPATH` allows direct imports from anywhere on the machine without hardcoding path modifications in scripts.

* **macOS / Linux (`~/.bash_profile` or `~/.bashrc`)**:
  ```bash
  export PYTHONPATH="/path/to/custom/modules"
  ```
* **Windows**:
  * Navigate to **System Properties** → **Advanced system settings** → **Environment Variables**.
  * Add a **New** User/System Variable named `PYTHONPATH` with the directory path as its value.

---

## 3. Exploring the Python Standard Library
The standard library comes built into Python, providing optimized, production-grade tools without requiring third-party package installations.

### 3.1 `random`
* Used for generating pseudo-random selections and values.

```python
import random

courses = ['History', 'Math', 'Physics', 'CompSci']
random_course = random.choice(courses)
print(random_course)
```

### 3.2 `math`
* Provides fundamental mathematical operations, trigonometric calculations, and constants.

```python
import math

rads = math.radians(90)
print(rads)            # Converts 90 degrees to radians
print(math.sin(rads))  # Output: 1.0
```

### 3.3 `datetime` and `calendar`
* Utilities for handling dates, timestamps, and calendar arithmetic.

```python
import datetime
import calendar

# Get current date
today = datetime.date.today()
print(today)

# Check leap year status
print(calendar.isleap(2020))  # True
print(calendar.isleap(2017))  # False
```

### 3.4 `os`
* Provides direct interfaces to interact with the underlying operating system and file system.

```python
import os

# Get current working directory
print(os.getcwd())
```

### 3.5 Locating Module Files (`__file__`) & `antigravity`
* Inspect where any imported module file physically lives on disk using the `__file__` dunder attribute:

```python
import os
print(os.__file__)
```

* **The `antigravity` Easter Egg**: A built-in module in Python that demonstrates module imports by leveraging the `webbrowser` standard module to open the classic Python comic:

```python
import antigravity
```

---

