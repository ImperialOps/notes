# Stack

A stack stores ordered items with top-only access.
- **LIFO**: last in, first out.
- Add/remove only at top.
- Middle/bottom access needs popping items above.

## Stack Speed

Stack behaves like restricted list. Restriction gives predictable speed.

| Operation | Big O | Description |
| --- | --- | --- |
| `push` | `O(1)` | Add item to top |
| `pop` | `O(1)` | Remove and return top item |
| `peek` | `O(1)` | Return top item without removal |
| `size` | `O(1)` | Return item count |

All core stack operations are **O(1)**.

## Notes

- Accessing deep item (near bottom) is **O(n)** because repeated `pop`.
- Stack interface is limited: no random access, no built-in search/sort.
- Stack can store any data type; behavior defines structure.

## Common Uses

- Function call management.
- Undo/redo.
- Expression evaluation.
- Browser history.

## Implementation Reference

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def size(self):
        return len(self.items)

    def peek(self):
        if not self.items:
            return None
        return self.items[-1]

    def pop(self):
        if not self.items:
            return None
        return self.items.pop()
```