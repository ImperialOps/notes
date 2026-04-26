# Sorting Algorithms

## Bubble Sort

Bubble sort basic sorting algorithm. Name from elements that "bubble up" to top.

Implementation reference:

```python
def bubble_sort(nums):
    swapping = True
    end = len(nums)
    while swapping:
        swapping = False
        for i in range(1, end):
            if nums[i - 1] > nums[i]:
                temp = nums[i - 1]
                nums[i - 1] = nums[i]
                nums[i] = temp
                swapping = True
        end -= 1
    return nums
```

### Best and Worst Case

* **Best case:** Pre-sorted data, bubble sort runs fast `O(n)`.
* **Worst case:** Reverse data, bubble sort runs slow `O(n^2)` (same class as random data).

Bubble sort uses two nested loops:

1. The Outer Loop: In worst case (reverse-sorted list), pass through whole list many times so each element "bubbles" to correct position. About `n` passes.
1. The Inner Loop: Each pass compares adjacent elements through list. Inner loop also runs about `n` times (technically one shorter each pass, still linear in `n`).

Loop `n` times inside loop `n` times: `n * n = n^2`.

#### Visualizing the Growth

List of 10 items: worst case about 100 comparisons (10 squared).
List of 20 items: not double work, about 400 comparisons (20 squared).
Quadratic growth makes bubble sort poor for large datasets vs quicksort or merge sort.

#### The “Best Case” Exception

Bubble sort "Best Case" is O(n) when list already sorted. `swapping` flag detects no swaps on first pass, exits early. Big O without qualifier usually means upper bound / worst case.


## Merge Sort

Merge sort recursive sorting algorithm. Much faster than bubble sort. Divide-and-conquer algorithm:

* **Divide:** split large problem into smaller problems, recursively solve.
* **Conquer:** combine smaller results to solve large problem.

#### The “log n” part (The Divide)

Count how many times list can split in half until single elements.

* 8 elements split to 4, then 2, then 1. Takes 3 steps.
* In math, $2^3 = 8$, same as $\log_2(8) = 3$.
Each `merge_sort` call halves input. Halving builds tree with height log n.

#### The “n” part (The Conquer)

At each tree level, call `merge()` function.

* `merge()` has `while` loop iterating elements from lists being combined.
* To merge halves into sorted list size $n$, function reads each of those $n$ elements once.

#### Putting it together

Have log n split levels. Each level does n work to merge. Multiply:

`n (work per level) * log n (number of levels) = O(n log n)`

Implementation reference:

```python
def merge_sort(nums):
    if len(nums) < 2:
        return nums
    first = merge_sort(nums[: len(nums) // 2])
    second = merge_sort(nums[len(nums) // 2 :])
    return merge(first, second)


def merge(first, second):
    final = []
    i = 0
    j = 0
    while i < len(first) and j < len(second):
        if first[i] <= second[j]:
            final.append(first[i])
            i += 1
        else:
            final.append(second[j])
            j += 1
    while i < len(first):
        final.append(first[i])
        i += 1
    while j < len(second):
        final.append(second[j])
        j += 1
    return final
```

### Pros:

* Fast: Merge sort much faster than bubble sort. O(n*log(n)) vs O(n^2).
* Stable: duplicate-key values keep original order after sort.

### Cons:

* Memory usage: many sorts use single array copy. Merge sort needs extra subarrays in memory.
* Recursive: many recursive calls; in many languages (like Python), can add performance penalty.


## Insertion Sort

Insertion sort builds sorted list one item at time. Much less efficient on large lists than merge sort because O(n^2), but often faster on small lists (not Big O, smaller constants).

Insertion sort Big O is `O(n^2)` (worst case).

Outer loop always runs `n` times. Inner loop depends on input order.

* **Best case:** Pre-sorted data, insertion sort runs very fast (`O(n)`) because inner loop rarely shifts.
* **Average case:** `O(n^2)` because inner loop runs about half-range on average.
* **Worst case:** Reverse data, still `O(n^2)` because inner loop runs full range each pass.

Implementation reference:

```python
def insertion_sort(nums):
    for i in range(len(nums)):
        j = i
        while j > 0 and nums[j - 1] > nums[j]:
            nums[j], nums[j - 1] = nums[j - 1], nums[j]
            j -= 1
    return nums
```

### Why Use Insertion Sort?

* **Fast on tiny inputs:** Often faster than merge sort and quicksort on very small lists.
* **Adaptive:** Faster when data is partially sorted.
* **Stable:** Equal-key elements keep relative order.
* **In-place:** Uses constant extra memory.
* **Online:** Can sort as new items arrive.

#### Why fast on small lists?

Many production sort implementations use insertion sort below small threshold (often around 10-ish), then switch to quicksort/merge sort for bigger inputs.

Reason:

* **No recursion overhead**
* **Tiny memory footprint**
* **Stable behavior**
