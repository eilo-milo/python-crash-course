# Python Iterators, Generators, Lambdas & Closures Reference Guide

---

## 1. The Iterator Protocol

In Python, an **iterable** is any object you can loop over, while an **iterator** is the engine that produces values on demand. Any class can act as an iterator by implementing two dunder methods:

* `__iter__()`: Invoked once when iteration starts; returns the iterator object itself (`self`).
* `__next__()`: Invoked on each loop step to fetch the next value. It signals the end of iteration by raising the `StopIteration` exception.

```python
class CountDown:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        val = self.current
        self.current -= 1
        return val


for num in CountDown(3):
    print(num)  # Outputs: 3, 2, 1
```

---

## 2. Generators and the `yield` Keyword

Writing a full class with `__iter__` and `__next__` requires boilerplate to track internal state. A generator provides an elegant syntax to implement the exact same protocol using a standard function:

* **`return` vs. `yield`:**
  * `return`: Terminates function execution completely and destroys its local execution frame.
  * `yield`: Pauses the function, passes a value back to the caller, and freezes the instruction pointer and all variable states until the next value is requested via `next()`.

```python
def fibonacci(n):
    p, pp = 1, 1
    for i in range(n):
        if i in (0, 1):
            yield 1
        else:
            p, pp = pp, p + pp
            yield p


print(list(fibonacci(6)))  # [1, 1, 2, 3, 5, 8]
```

### List Comprehensions vs. Generator Expressions

* `[x * 2 for x in range(1000)]` (Square Brackets): Builds and populates the entire list in memory immediately (**eager evaluation**).
* `(x * 2 for x in range(1000))` (Parentheses): Produces values sequentially on demand (**lazy evaluation**), minimizing memory overhead.

---

## 3. Anonymous Functions (`lambda`), `map()`, and `filter()`

A `lambda` is an inline, single-expression function defined without a formal name:

$$\text{Syntax: } \lambda \text{ arguments : expression}$$

* `map(function, iterable)`: Applies the function to every item in the sequence and returns an iterator of the transformed values.
* `filter(function, iterable)`: Passes each item through a boolean predicate; retains only elements where the predicate evaluates to `True`.

```python
nums = [1, 2, 3, 4, 5, 6]

# Map: double every value
doubled = list(map(lambda x: x * 2, nums))
# Output: [2, 4, 6, 8, 10, 12]

# Filter: keep only even values
evens = list(filter(lambda x: x % 2 == 0, nums))
# Output: [2, 4, 6]
```

---

## 4. Closures

A **closure** is a nested function that preserves access to variables in its outer enclosing scope even after the outer function has completed execution and returned.

### Three Requirements for a Closure
1. A nested function (a function defined inside another function).
2. The inner function references at least one variable in the outer enclosing scope.
3. The outer function returns the inner function object itself (without calling it with `()`).

```python
def make_multiplier(factor):
    # 'factor' is stored in the closure's cell memory
    def multiply(number):
        return number * factor
    return multiply


double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))  # 10 (remembers factor = 2)
print(triple(5))  # 15 (remembers factor = 3)
```

> **Note:** Closures form the underlying architectural foundation for **Python Decorators**.
