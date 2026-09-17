

---

## 1. Core Concepts Breakdown

### The Iterator Protocol
A formal protocol that allows custom objects to interface with iteration contexts (such as `for ... in` loops, list constructors, and sequence unpacking).

* `__iter__()`: Returns the iterator object itself. It is invoked once at the initialization of the iteration loop.
* `__next__()`: Returns the next sequential element on each invocation. Once all values are exhausted, it must raise the `StopIteration` exception to signal termination.

---

### Generators & The `yield` Keyword
* **Generator Function:** Any function containing the `yield` statement. Calling a generator function does not run the body immediately; instead, it returns a generator iterator object.
* **`yield` vs. `return`:**
  * `return`: Terminates function execution permanently, destroys local state, and passes a single value back to the caller.
  * `yield`: Produces a value, pauses execution, and suspends the entire stack frame (local variables, execution pointer) until the next value is requested via `next()`.
* **Generator Expressions:** Declared using parentheses instead of brackets: `(x * 2 for x in range(5))`. Computes values lazily on demand rather than eagerly constructing the entire sequence in memory.

---

### Lambda Functions
* **Syntax:** `lambda parameters: expression`
* **Characteristics:** Anonymous, inline functions restricted to a single evaluated expression whose result is implicitly returned.
* **Primary Use Case:** Passing lightweight callbacks directly into higher-order functions without declaring formal `def` functions.

---

### Higher-Order Processing Functions
* `map(function, iterable)`: Applies `function` to each element in `iterable` and yields an iterator of transformed values.
* `filter(function, iterable)`: Evaluates `function(item)` for each element and yields an iterator containing only elements where the predicate returns a truthy value (`True`).

---

### Closures
* **Definition:** A nested function that retains direct access to variables from its enclosing lexical scope, even after the outer enclosing function has completed execution and returned.
* **Mechanism:** The nested function bundles and references variables in its parent scope (`__closure__`), allowing persistent state retention without global variables.

---

## 2. Reconstructed Code Examples

### Example A: Object-Oriented Fibonacci Iterator (Direct Implementation)

```python
class Fib:
    def __init__(self, nn):
        print("__init__")
        self.__n = nn
        self.__i = 0
        self.__p1 = self.__p2 = 1

    def __iter__(self):
        print("__iter__")
        return self

    def __next__(self):
        print("__next__")
        self.__i += 1
        if self.__i > self.__n:
            raise StopIteration
        if self.__i in [1, 2]:
            return 1
        ret = self.__p1 + self.__p2
        self.__p1, self.__p2 = self.__p2, ret
        return ret


for i in Fib(10):
    print(i)
```

---

### Example B: Iterator Composed into Another Class

```python
class Fib:
    def __init__(self, nn):
        self.__n = nn
        self.__i = 0
        self.__p1 = self.__p2 = 1

    def __iter__(self):
        return self

    def __next__(self):
        self.__i += 1
        if self.__i > self.__n:
            raise StopIteration
        if self.__i in [1, 2]:
            return 1
        ret = self.__p1 + self.__p2
        self.__p1, self.__p2 = self.__p2, ret
        return ret


class Class:
    def __init__(self, n):
        self.__iter = Fib(n)

    def __iter__(self):
        return self.__iter


obj = Class(10)
for i in obj:
    print(i)
```

---

### Example C: List Comprehension with Conditional Expressions

```python
# Routine loop vs. list comprehension
lst1 = []
for x in range(6):
    lst1.append(10 ** x)

lst2 = [10 ** x for x in range(6)]
print(lst1)
print(lst2)

# List comprehension using conditional expression (1 if even index, else 0)
alternating = [1 if x % 2 == 0 else 0 for x in range(10)]
print(alternating)
```

---

### Example D: Higher-Order Functions (`map` and `filter`) with Lambdas

```python
import random

# Using map() with lambdas
list_1 = [x for x in range(5)]
list_2 = list(map(lambda x: 2 ** x, list_1))
print(list_2)

for x in map(lambda x: x ** 2, list_2):
    print(x, end=" ")
print()

# Using filter() with lambdas
random.seed(0)
data = [random.randint(-10, 10) for _ in range(5)]
filtered = list(filter(lambda x: x > 0 and x % 2 == 0, data))

print(data)
print(filtered)
```
