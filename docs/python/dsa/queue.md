# Queue

A queue stores ordered items with two ends: **tail** and **head**.
- **FIFO**: first in, first out.
- New items enter at tail (end/rear).
- Old items leave from head (front).
- Oldest item leaves first.

## Queue Speed (List-Based)

Speeds below assume Python `list` implementation.

| Operation | Big O | Description |
| --- | --- | --- |
| `enqueue` | `O(1)` amortized | Add item to tail with `append()` |
| `dequeue` | `O(n)` | Remove head with `pop(0)` (elements shift left) |
| `peek` | `O(1)` | Return head with `items[0]` |
| `size` | `O(1)` | Return item count |

FIFO behavior still same: first item in, first item out.

## Notes

- `enqueue` = add to tail. `dequeue` = remove from head.
- With Python list, `pop(0)` shifts remaining elements, so `dequeue` is **O(n)**.
- Use `collections.deque` for stable **O(1)** enqueue/dequeue.
- Queue can store any data type; behavior defines structure.

## Common Uses

- Task scheduling.
- Breadth-first search (BFS).
- Message/job processing.
- Print queue.

## Implementation Reference

```python
class Queue:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.insert(0, item)

    def pop(self):
        if not self.items:
            return None
        item = self.items[-1]
        del self.items[-1]
        return item

    def peek(self):
        if not self.items:
            return None
        return self.items[-1]

    def size(self):
        return len(self.items)
```
