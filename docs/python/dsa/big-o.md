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
