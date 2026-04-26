# Sorting Algorithms

## Bubble Sort

Bubble sort is a very basic sorting algorithm named for the way elements "bubble up" to the top of the list.

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

* **Best case:** If the data is pre-sorted, bubble sort becomes really fast `O(n)`.
* **Worst case:** If the data is in reverse order, bubble sort becomes really slow `O(n^2)` (but still in the same complexity class as random data).

Bubble sort relies on two nested layers of iteration:

1. The Outer Loop: In the worst-case scenario (like a reverse-sorted list), we have to pass through the entire list multiple times to ensure every element "bubbles" to its correct position. In the worst case, this happens approximately `n` times.
1. The Inner Loop: During each of those passes, we iterate through the list to compare adjacent elements. This inner loop also runs approximately `n` times (though it technically gets shorter by one each time, it still scales linearly with `n`).

When you have a loop running `n` times inside another loop that runs `n` times, you multiply the complexities: `n * n = n^2`.

#### Visualizing the Growth

Imagine a list of 10 items. In the worst case, you might perform roughly 100 comparisons (10 squared).
If you double the list to 20 items, you aren't just doubling the work; you're performing roughly 400 comparisons (20 squared).
This quadratic growth is what makes bubble sort inefficient for large datasets compared to algorithms like quicksort or merge sort.

#### The “Best Case” Exception

It is worth noting that bubble sort has a "Best Case" time complexity of O(n). This happens if the list is already sorted. The `swapping` flag in the implementation allows the algorithm to realize no swaps were made during the first pass and exit early. However, when we talk about the "Big O" of an algorithm without qualifiers, we are usually referring to the upper bound or worst-case scenario.


## Merge Sort

Merge sort is a recursive sorting algorithm and it's quite a bit faster than bubble sort. It's a divide and conquer algorithm.:

* **Divide:** divide the large problem into smaller problems, and recursively solve the smaller problems
* **Conquer:** Combine the results of the smaller problems to solve the large problem

#### The “log n” part (The Divide)

Think about how many times you can split a list in half until you reach individual elements.

* If you have 8 elements, you split it into 4, then 2, then 1. That took 3 steps.
* In mathematics, $2^3 = 8$, which is the same as saying $\log_2(8) = 3$.
Every time we recursively call `merge_sort`, we are halving the input. This "halving" process creates a tree with a height of log n.

#### The “n” part (The Conquer)

At each level of that tree, we have to call the `merge()` function.

* The `merge()` function contains a `while` loop that iterates through the elements of the lists it is combining.
* To merge two halves back into a single sorted list of size $n$, the function has to look at every single one of those $n$ elements once.

#### Putting it together

Since we have log n levels of splitting, and at each level, we perform n amount of work to merge the pieces back together, we multiply them:

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

* Fast: Merge sort is much faster than bubble sort. O(n*log(n)) instead of O(n^2).
* Stable: Merge sort is a stable sort which means that values with duplicate keys in the original list will be in the same order in the sorted list.

### Cons:

* Memory usage: Most sorting algorithms can be performed using a single copy of the original array. Merge sort requires extra subarrays in memory.
* Recursive: Merge sort requires many recursive function calls, and in many languages (like Python), this can incur a performance penalty.


## Insertion Sort

Insertion sort builds a sorted list one item at a time. It's much less efficient on large lists than merge sort because it's O(n^2), but it's actually faster (not in Big O terms, but due to smaller constants) than merge sort on small lists.

