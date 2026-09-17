1. The Iterator ProtocolIn Python, an iterable is any object you can loop over, while an iterator is the engine that produces values on demand. Any class can act as an iterator by implementing two dunder methods:__iter__(): Invoked once when iteration starts; returns the iterator object itself (self).__next__(): Invoked on each loop step to fetch the next value. It signals the end of iteration by raising the StopIteration exception.Pythonclass CountDown:
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
2. Generators and the yield KeywordWriting a full class with __iter__ and __next__ requires boilerplate to track internal state. A generator provides an elegant syntax to achieve the exact same protocol using a regular function:return vs. yield:return terminates function execution completely and cleans up its local scope.yield pauses the function, outputs a value to the caller, and freezes the execution pointer and all variable states until the next call.Pythondef fibonacci(n):
    p, pp = 1, 1
    for i in range(n):
        if i in (0, 1):
            yield 1
        else:
            p, pp = pp, p + pp
            yield p

print(list(fibonacci(6)))  # [1, 1, 2, 3, 5, 8]
List Comprehensions vs. Generator Expressions:[x * 2 for x in range(1000)] (Square brackets): Builds the entire list in memory immediately (eager evaluation).(x * 2 for x in range(1000)) (Parentheses): Produces values one at a time on demand (lazy evaluation), consuming almost no RAM.3. Anonymous Functions (lambda), map(), and filter()A lambda is an inline, single-expression function without a formal name:$$\text{Syntax: } \lambda \text{ arguments : expression}$$map(function, iterable): Applies the function to every item in the sequence and returns an iterator of results.filter(function, iterable): Evaluates each item through a boolean predicate; retains only items that evaluate to True.Pythonnums = [1, 2, 3, 4, 5, 6]

# Map: double every value
doubled = list(map(lambda x: x * 2, nums))
# Output: [2, 4, 6, 8, 10, 12]

# Filter: keep only even values
evens = list(filter(lambda x: x % 2 == 0, nums))
# Output: [2, 4, 6]
4. ClosuresA closure is an inner function that retains access to variables in its enclosing (outer) function's scope even after the outer function has finished executing and returned.Three Requirements for a Closure:A nested function (a function inside a function).The inner function references a variable in the outer function's scope.The outer function returns the inner function object itself (without calling it with parentheses).Pythondef make_multiplier(factor):
    # 'factor' is stored in the closure's cell memory
    def multiply(number):
        return number * factor
    return multiply

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))  # 10 (remembers factor = 2)
print(triple(5))  # 15 (remembers factor = 3)
Closures form the underlying theoretical foundation for Python Decorators.
