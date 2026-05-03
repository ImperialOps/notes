# Sorting Algorithms

## Bubble Sort

Basic algorithm. Tiny value float up toward end like bubbles.

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

* **Best case:** Already sorted → fast `O(n)`.
* **Worst case:** Reversed → slow `O(n^2)` (random-ish data same class).

Two nested loops:

1. **Outer:** Worst case you sweep whole list many times so values "bubble" to right slots. Roughly `n` passes.
2. **Inner:** Each sweep compares neighbors. Roughly `n` comparisons per sweep (each pass shorter by one — still scales like `n`).

Outer `n`, inner `n` → multiply → `n^2`.

#### Visualizing the Growth

* 10 items, worst ~100 comparisons (`10²`).
* 20 items → not double work → ~400 (`20²`).
* Quadratic = bad at big lists vs merge sort / quicksort.

#### “Best Case” Exception

Sorted list → best case `O(n)`. `swapping` flag notices zero swaps after first pass → stop early.

Unqualified Big O usually means worst / upper bound.

## Merge Sort

Recursive divide-and-conquer. Faster than bubble in practice.

* **Divide:** chop problem, recurse small pieces.
* **Conquer:** merge sorted pieces back together.

#### “log n” part (divide)

Halve list until singletons.

* 8 → 4 → 2 → 1 → 3 splits.
* $2^3 = 8$ — same fact as $\log_2(8) = 3$.

Every `merge_sort` call halves range → tree depth ~log n.

#### “n” part (conquer)

Each depth level runs `merge()`.

* `merge()` loops with `while` over both halves.
* Merging into size-$n$ output touches each element once → `O(n)` work that level.

#### Putting it together

log n levels, `n` work per level → multiply:

`n (work per level) * log n (levels) = O(n log n)`

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

### Pros

* **Speed:** Usually `O(n log n)`, smokes `O(n²)` bubble on big inputs.
* **Stable:** Duplicate keys keep original relative order.

### Cons

* **Memory:** Needs extra buffers; not like one-array-only sorts.
* **Recursion:** Deep calls hurt some runtimes (e.g. Python).

## Insertion Sort

Grow sorted prefix one element at front. Large lists: worse than merge (`O(n²)`). Tiny lists: often wins anyway (constants win over Big-O story).

Worst-case Big-O: `O(n²)`.

Outer loop `n` times always. Inner loop length depends how messy data is.

* **Best case:** Already sorted → `O(n)`, inner barely shifts.
* **Average case:** `O(n²)` — inner walks ~half gap on typical mix.
* **Worst case:** Reversed → `O(n²)` — inner walks full gap every time.

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

* **Fast on tiny n:** Often beats merge/quicksort on very small spans.
* **Adaptive:** Nearly sorted → less inner work.
* **Stable:** Equal keys stay in order.
* **In-place:** `O(1)` extra beyond array.
* **Online:** Slide new items into sorted prefix as they arrive.

#### Why prod uses it on small chunks

Libs often run insertion sort under small threshold (~10-ish), swap to quicksort / merge beyond that:

* No recursion tax
* Tiny memory footprint
* Still stable (if you pick stable merge variant elsewhere)

## Quick Sort

Popular recursive divide-and-conquer. Real systems add tricks (median-of-three, insertion on small tails, etc.) — below is naive shape.

### Divide

* **Pick pivot** — want near middle of sorted outcome (median ideal).
* **Partition** — shove `< pivot` left, `> pivot` right.
* **Pivot settles** — one index now final.
* **Recurse** — repeat on left and right subranges.

### Conquer

When every region finished partitioning → whole array sorted.

Implementation reference:

```python
def quick_sort(nums, low, high):
    if low < high:
        p = partition(nums, low, high)
        quick_sort(nums, low, p - 1)
        quick_sort(nums, p + 1, high)


def partition(nums, low, high):
    pivot = nums[high]
    i = low
    for j in range(low, high):
        if nums[j] < pivot:
            nums[i], nums[j] = nums[j], nums[i]
            i += 1
    nums[i], nums[high] = nums[high], nums[i]
    return i
```

### Complexity sketch

Average: `O(n log n)`. Naive worst (bad pivots): `O(n²)`.

`partition()` scans `low..high` once → `O(n)` per invocation.

Bill = (#partition calls) × `O(n)`.

**Worst case shaped like:** already sorted input + pivot always smallest or biggest each step → skinny recursion tree → ~`n` partition layers → `n × n`.

**Best split shaped like:** pivot near median each time → tree depth ~`log n` → `n log n`.
