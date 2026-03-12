# 🧩 Functional Programming in Python

Functional programming (FP) is a paradigm that treats computation as the evaluation of mathematical functions and avoids changing-state or mutable data.

---

## 🛠 The "Big Three"

These functions allow you to process data without using explicit `for` loops.

### 1. Map

Applies a function to every item in an iterable.

```python
numbers = [1, 2, 3, 4, 5]

# Using lambda to square each number
squared = list(map(lambda x: x**2, numbers))
# Output: [1, 4, 9, 16, 25]
```

### 2. Filter

Filters items based on a condition (must return `True` or `False`).

```python
numbers = range(10)

# Keep only even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))
# Output: [0, 2, 4, 6, 8]
```

### 3. Reduce

Performs a rolling computation on sequential pairs of values to return a **single** value.

!!! note "Import Required"
    In Python 3, `reduce` was moved to the `functools` module.

```python
from functools import reduce

# Factorial Example: 5! = (5 * 4 * 3 * 2 * 1)
n = 5
factorial = reduce(lambda x, y: x * y, range(1, n + 1))
# Output: 120
```

---

## 🧪 Pure Functions

A function is **pure** if it:

1. Returns the same output for the same input every time.
2. Has **no side effects** (it doesn't change global variables or modify the input list).

```python
# Pure: Result depends only on inputs
def multiply(a, b):
    return a * b

# Impure: Modifies an external variable (side effect)
total = 0
def add_to_total(n):
    global total
    total += n
```

---

## 🍛 Currying

Currying is the practice of breaking down a function that takes multiple arguments into a series of functions that each take a single argument.

```python
def multiply(a):
    def with_b(b):
        return a * b
    return with_b

# Usage
double = multiply(2)
print(double(10)) # Output: 20
```

---

## 🎨 Decorators

Decorators allow you to "wrap" another function to extend its behavior without permanently modifying it. This is a primary pattern in Python web frameworks and AWS Lambda logic.

```python
def debug_log(func):
    def wrapper(*args, **kwargs):
        print(f"Executing {func.__name__}...")
        result = func(*args, **kwargs)
        print("Finished execution.")
        return result
    return wrapper

@debug_log
def say_hi(name):
    return f"Hi {name}"

# Output:
# Executing say_hi...
# Finished execution.
# 'Hi [name]'
```

---

### 🚀 List Comprehensions vs. Map/Filter

In Python, "Pythonic" code usually favors readability and speed. Here is how to choose the right tool for the job.

#### 1. Use List Comprehensions When...

- **The logic is simple:** `[x**2 for x in nums]` is unbeatable for clarity.
- **You need readability:** It reads like a natural sentence from left to right.
- **You need speed:** For simple operations, the internal C-optimization of comprehensions beats the overhead of a Python `lambda` call.

#### 2. Use `map()` or `filter()` When...

- **You have a named function:** ✅ **Good:** `map(int, list_of_strings)`
- ❌ **Redundant:** `[int(x) for x in list_of_strings]`
- **You need Lazy Evaluation:** If you have a 10GB dataset, `map` creates an **iterator**. It processes items one-by-one only as you request them. A list comprehension `[]` would attempt to load all 10GB into RAM immediately and crash the program.

---

### 📊 Comparison Summary

| Tool               | Result Type | Evaluation       | Memory Usage | Best For...                                          |
| :----------------- | :---------- | :--------------- | :----------- | :--------------------------------------------------- |
| **List Comp** `[]` | List        | **Eager** (Now)  | High         | Small/Medium data, speed, readability.               |
| **Generator** `()` | Iterator    | **Lazy** (Later) | **Minimal**  | Massive datasets, infinite streams.                  |
| **Map / Filter**   | Iterator    | **Lazy** (Later) | **Minimal**  | Using existing named functions (e.g., `int`, `len`). |

---

### 💡 The "Pro" Interview Answer

If an interviewer asks how to handle a 100GB file without crashing, you describe **Lazy Evaluation**. You explain that while a List Comprehension is faster for small tasks, a **Generator Expression** or **`map()`** is required for memory safety because they yield one item at a time.
