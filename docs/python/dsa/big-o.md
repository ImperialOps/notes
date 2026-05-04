# Big O

Many algorithms exist — fast, slow, greedy on memory. Picking one for problem gets fuzzy fast.

**Big O** analysis (say "Big Oh", not "Big Zero") ranks algorithms by **worst-case growth** of time or space vs input size.

> Big O tags algorithms by worst-case growth rate.

Notation:

```
O(formula)
```

Say **order** *formula*. `formula` = how runtime or memory blows up as `n` grows.

* `O(1)` — constant
* `O(log n)` — logarithmic
* `O(n)` — linear
* `O(n^2)` — squared
* `O(2^n)` — exponential
* `O(n!)` — factorial

Chart: `x` = input size, `y` = work / time.

![Big O chart](https://cdn-media-1.freecodecamp.org/images/1*KfZYFUT2OKfjekJlCeYvuQ.jpeg)

## Exponential Time

Rough split:

* Polynomial time
* Exponential time

![Exponential Time](https://storage.googleapis.com/qvault-webapp-dynamic-assets/course_assets/dAYrqF4-1086x720.png)

(`O(n!)` is factorial — lump with exponentials here for intuition.)

**Polynomial:** runtime grows no faster than `n^k` for fixed `k` (`n²`, `n³`, …). Usable if exponent / constants stay tame.

**Exponential:** usually impractical for serious `n`. Crypto sometimes *wants* that pain. Tiny `n`: still explodes — `n = 20` → `2^n` already past million.

| n | n^2 | 2^n |
| --- | --- | --- |
| 2 | 4 | 4 |
| 3 | 9 | 8 |
| 4 | 16 | 16 |
| 5 | 25 | 32 |
| 6 | 36 | 64 |
| 7 | 49 | 128 |
| 8 | 64 | 256 |
| 9 | 81 | 512 |
| 10 | 100 | 1024 |
| 11 | 121 | 2048 |
| 12 | 144 | 4096 |
| 13 | 169 | 8192 |
| 14 | 196 | 16384 |
| 15 | 225 | 32768 |
| 16 | 256 | 65536 |
| 17 | 289 | 131072 |
| 18 | 324 | 262144 |
| 19 | 361 | 524288 |
| 20 | 400 | 1048576 |

### Polynomial Time = P

1970s naming: class **P** = problems solvable in polynomial time.

* **In P:** tractable on normal computers.
* **Outside P:** often brutal / impractical at scale.

### Turning Fibonacci Polynomial

Take exponential-style Fibonacci naïveté → rewrite → polynomial-time iteration.

Fibonacci: each term = sum of two before:

```
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
```

Want `fib(index)`:

* `fib(0)` -> 0
* `fib(1)` -> 1
* `fib(2)` -> 1
* `fib(3)` -> 2
* `fib(4)` -> 3
* `fib(5)` -> 5
* `fib(6)` -> 8
* `fib(7)` -> 13

Iterative version:

```python
def fib(n):
    if n <= 1:
        return n
    current = 0
    parent = 1
    grandparent = 0
    for _ in range(0, n - 1):
        current = parent + grandparent
        grandparent = parent
        parent = current
    return current
```

## Big O Review

| **Big-O** | Name | Description |
| --- | --- | --- |
| **O(1)** | constant | **Best** The algorithm always takes the same amount of time, regardless of how much data there is. Example: Looking up an item in a list by index |
| **O(log(n))** | logarithmic | **Great** Algorithms that remove a percentage of the total steps with each iteration. Very fast, even with large amounts of data. Example: Binary search |
| **O(n)** | linear | **Good** 100 items, 100 units of work. 200 items, 200 units of work. This is usually the case for a single, non-nested loop. Example: unsorted array search. |
| **O(n\*log(n))** | linearithmic | **Okay** This is slightly worse than linear, but not too bad. Example: mergesort and other "fast" sorting algorithms. |
| **O(n^2)** | quadratic | **Slow** The amount of work is the square of the input size. 10 inputs, 100 units of work. 100 Inputs, 10,000 units of work. Example: A nested for loop to find all the ordered pairs in a list. |
| **O(n^3)** | cubic | **Slower** If you have 100 items, this does 100^3 = 1,000,000 units of work. Example: A triple nested for loop to find all the ordered triples in a list. |
| **O(2^n)** | exponential | **Horrible** We want to avoid this kind of algorithm at all costs. Adding one to the input doubles the amount of steps. Example: Brute-force guessing results of a sequence of `n` coin flips. |
| **O(n!)** | factorial | **Even More Horrible** The algorithm becomes so slow so fast, that it is practically unusable. Example: Generating all the permutations of a list |

### Complexity Quiz

```python
#  halvedSections returns a list of lists.
#  For example, n=12 results in:
#    [
#       [0 1 2 3 4 5 6 7 8 9 10 11 12]
#       [0 1 2 3 4 5 6]
#       [0 1 2 3]
#       [0 1]
#    ]
def halved_sections(n):
    rows = []
    i = n
    while i > 0:
        col = []
        for j in range(i+1):
            col.append(j)
        rows.append(col)
        i //= 2
    return rows
```

Specific time complexity:

`T(n) = O(n + n/2 + n/4 + ... 1)`

* **Equivalent (not fully reduced):** `T(2n)`
* **Most reduced:** `T(n)`

`halved_sections` builds many rows. Total cost = total append work across loops.

Each `while` pass halves `i`. Inner `for` runs `i + 1` times to build row.

Starting from `n`, append count pattern:

* **Row 1:** `n`
* **Row 2:** `n/2`
* **Row 3:** `n/4`
* **...**
* **Last row:** `1`

Total work = geometric series: `n + n/2 + n/4 + n/8 + ... + 1`.

Series stays below `2n`, approaches it from below. Example:

* `1 + 0.5 = 1.5`
* `1 + 0.5 + 0.25 = 1.75`
* `1 + 0.5 + 0.25 + 0.125 = 1.875`

So total ops < `2n` -> equivalent form `O(2n)`. Drop constant in reduced Big O -> `O(n)`.

Quiz asks equivalent (not fully reduced) form, so `O(2n)` is target.