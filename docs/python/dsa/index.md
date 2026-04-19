# Data Structures and Algorithms

### What Is a Data Structure?

Data structures are just organizational tools that allow for more advanced algorithms.

### What Is an Algorithm?

An algorithm is a finite sequence of well-defined, computer-implementable instructions. In short, an algorithm is:

* **Defined:** there is a specific sequence of steps that performs a task
* **Unambiguous:** there is a "correct" and "incorrect" interpretation of the steps
* **Implementable:** it can be executed using software and hardware

## Math

### Exponents

An exponent indicates how many times a number is to be multiplied by itself. For example:

$5^3$ = `5 * 5 * 5` = `125`

```python
square = 2 ** 2
# square = 4

cube = 2 ** 3
# cube = 8
```

### Logarithms

A logarithm is the **inverse of an exponent**. While exponents grow numbers very quickly, logarithms shrink them, making them essential for calculating **Time Complexity**.

#### The Core Concept

If $2^4 = 16$, then the logarithm is the answer to the question: *"To what power must we raise 2 to get 16?"*

* **Exponential:** $2^4 = 16$
* **Logarithmic:** $\log_2(16) = 4$

> "$\log_2(16)$" is read as **"log base 2 of 16"**. It means "the number of times 2 must be multiplied by itself to equal 16."

---

#### Logarithm Cheat Sheet

| Logarithm | Result | Exponential Equivalent |
| :--- | :---: | :--- |
| $\log_2(2)$ | **1** | $2^1 = 2$ |
| $\log_2(4)$ | **2** | $2^2 = 4$ |
| $\log_2(8)$ | **3** | $2^3 = 8$ |
| $\log_2(16)$ | **4** | $2^4 = 16$ |
| $\log_{10}(10)$ | **1** | $10^1 = 10$ |
| $\log_{10}(100)$ | **2** | $10^2 = 100$ |
| $\log_{10}(1000)$ | **3** | $10^3 = 1000$ |
| $\log_{10}(10000)$ | **4** | $10^4 = 10000$ |

---

#### Why This Matters for Big O

In Big O notation, we usually assume **base 2**. When you see **O(log n)**, it means the algorithm reduces the problem size by half in every step (e.g., Binary Search).

* If $n = 1,000,000$, a linear $O(n)$ search takes **1,000,000 steps**.
* A logarithmic $O(\log n)$ search takes only **~20 steps**.
