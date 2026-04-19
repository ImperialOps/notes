# Sorting Algorithms

## Bubble Sort O(n^2)

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

In merge sort we:

* Divide the array into two (equal) halves (divide)
* Recursively sort the two halves
* Merge the two halves to form a sorted array (conquer)

