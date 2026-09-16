

---

## 1. Inspecting Modules with `dir()`

The built-in function `dir()` returns an alphabetically sorted list of strings representing all accessible attributes, functions, classes, and metadata within an imported entity.

```python
import math

# Returns list of strings: ['__doc__', '__name__', 'acos', 'ceil', 'pi', ...]
entities = dir(math)

# If aliased, dir() must target the alias name:
import math as m
entities = dir(m)
```

* **Dunder Names:** Attributes wrapped in leading/trailing double underscores (e.g., `__name__`, `__doc__`) represent internal module metadata.
* **Scope Restriction:** `dir()` operates on module references loaded into the active namespace. If you use `from module import entity`, only that specific entity enters the local namespace; running `dir(module)` will raise a `NameError`.

---

## 2. Core Standard Library Modules

### The `math` Module
Focuses on low-level, high-performance floating-point mathematical operations:

* **Trigonometry (Radian-based):** `sin(x)`, `cos(x)`, `tan(x)`, and their inverse variants `asin(x)`, `acos(x)`, `atan(x)`.
* **Angle Conversions:** `radians(degrees)` converts degrees $\to$ radians; `degrees(radians)` converts radians $\to$ degrees.
* **Constants:** `math.pi` ($\approx 3.141592...$), `math.e` ($\approx 2.718281...$).
* **Exponents & Logarithms:**
  * `exp(x)`: Evaluates $e^x$.
  * `log(x)`: Natural logarithm ($\ln(x)$).
  * `log(x, b)`: Base-$b$ logarithm ($\log_b(x)$).
  * `log10(x)`, `log2(x)`: Optimized variants for base-10 and base-2 calculations.
  * *Note:* The built-in `pow(x, y)` evaluates exponents using integer or float arithmetic, whereas `math.pow(x, y)` always casts inputs and returns a float.

#### Integer Truncation & Rounding

| Function | Definition | Example (`x = 2.7`) | Example (`x = -2.7`) |
| :--- | :--- | :--- | :--- |
| `math.ceil(x)` | Smallest integer $\ge x$ | `3` | `-2` |
| `math.floor(x)` | Largest integer $\le x$ | `2` | `-3` |
| `math.trunc(x)` | Truncates fractional component toward zero | `2` | `-2` |

---

### The `random` Module
Implements pseudo-random number generators (PRNGs) governed by deterministic internal state seeds.

```python
import random

# Initialize generator state; defaults to system clock if omitted
random.seed(42)

# Floating point in [0.0, 1.0)
val = random.random()

# Integers:
# randrange mirrors range() syntax -> half-open interval [start, stop)
r_range = random.randrange(1, 10, 2)  # Generates 1, 3, 5, 7, or 9

# randint includes BOTH boundaries -> closed interval [start, stop]
r_int = random.randint(1, 10)         # 1 <= r_int <= 10

# Sequences:
seq = [10, 20, 30, 40, 50]
single_item = random.choice(seq)      # Single pick (with replacement)
sample_list = random.sample(seq, 3)   # 3 UNIQUE elements (without replacement)
```

---

### The `platform` Module
Accesses underlying hardware platform configurations, OS layers, and runtime release specifications.

```python
import platform

platform.platform(aliased=False, terse=False)  # Full OS signature string
platform.machine()                             # Architecture: e.g., 'x86_64', 'armv7l'
platform.processor()                           # Exact CPU model string
platform.system()                              # Generic OS name: 'Windows', 'Linux', 'Darwin'
platform.version()                             # Underlying OS build/kernel release
platform.python_implementation()               # Engine name: 'CPython', 'PyPy'
platform.python_version_tuple()                # ('3', '10', '12') -> (major, minor, patch)
```

---

## 3. Writing Custom Modules

A custom module is a standalone `.py` script exposing variables, functions, and classes across other runtime scripts.

### Module Lifecycle & `__pycache__`
* **Bytecode Compilation:** Upon first import, Python parses source code into bytecode stored as `.pyc` files inside a local `__pycache__/` folder (e.g., `module.cpython-310.pyc`).
* **Cache Revalidation:** Subsequent launches cross-reference modification timestamps between the source file and bytecode. Python bypasses compilation if timestamps align.
* **Execution Caching:** Top-level logic executes **only once** on initial import. Subsequent imports retrieve existing references straight from `sys.modules`.

### The `__name__` Pattern
Every Python runtime module maintains a contextual `__name__` namespace variable:
* Executed as script root: `__name__ == "__main__"`
* Executed as imported dependency: `__name__ == "module_filename_without_ext"`

```python
# math_helpers.py
__counter = 0  # Leading underscore designates internal / private implementation

def add(a, b):
    global __counter
    __counter += 1
    return a + b

# Isolated unit test guard:
if __name__ == "__main__":
    assert add(2, 3) == 5
    print("Self-tests passed.")
```

### Search Path Resolution: `sys.path`
When resolving an `import xyz` call, Python queries paths in order through the `sys.path` list:
1. Current script working directory.
2. `PYTHONPATH` environment paths.
3. Standard library paths and active virtual environment `site-packages`.

```python
import sys
from pathlib import Path

# Add custom absolute or relative directory dynamically
sys.path.append(str(Path(__file__).resolve().parent / "modules"))

# Import directly from packaged ZIP files
sys.path.append("libs/extrapack.zip")
import custom_module
```

---

## 4. Structuring Packages

Packages group multiple interdependent module files through directory hierarchies using dotted module namespaces (e.g., `package.subpackage.module`).

### Directory Layout

```text
extra/
├── __init__.py          <-- Marks 'extra' as a Python package
├── iota.py
├── good/
│   ├── __init__.py      <-- Marks 'good' as a subpackage
│   ├── alpha.py
│   ├── beta.py
│   └── best/
│       ├── __init__.py  <-- Marks 'best' as a subpackage
│       ├── sigma.py
│       └── tau.py
└── ugly/
    ├── __init__.py
    ├── psi.py
    └── omega.py
```

* **The `__init__.py` Anchor:** Executes automatically during package initialization. Can remain empty, initialize package-wide states, expose clean public aliases, or limit wildcard imports with `__all__`.
* **Qualified Access:** Navigate directory depths using dot notation:

```python
from extra.good.best.tau import funT
import extra.good.best.sigma as sig

val_t = funT()
val_s = sig.funS()
```

---

## 5. Logical Operators (`and`, `or`, `not`)

Logical operators evaluate whole expressions using short-circuit boolean semantics without inspecting raw bits.

* `and` (Conjunction): Returns `True` only when both operands evaluate to `True`. Priority is lower than relational comparison operators.
* `or` (Disjunction): Returns `True` if either operand evaluates to `True`. Priority is lower than `and`.
* `not` (Negation): High-priority unary operator flipping truth values.
* **Assignment Shortcuts:** There are **no** inplace assignment shorthand operators for logical statements (e.g., `and=` or `or=` are invalid syntax).
* **Truth Value Rule:** Non-zero integers equate to `True`; `0` equates to `False`. Thus, `not not i` evaluates to `True` for any non-zero integer `i`.

### De Morgan's Laws in Python
```python
not (p and q) == (not p) or (not q)
not (p or q) == (not p) and (not q)
