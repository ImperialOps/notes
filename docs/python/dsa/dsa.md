# Data Structures

Data structures:
- Store data.
- Organize data for efficient access and updates.
- Expose operations to read/modify data.

Common types:
- **Stacks:** Last in, first out.
- **Queues:** First in, first out.
- **Linked Lists:** Node chain; efficient inserts/deletes.
- **Binary Trees:** Each node has up to two children.
- **Red-Black Trees:** Self-balancing binary tree.
- **Hashmaps:** Map keys to values.
- **Tries:** Efficient word/prefix storage and lookup.
- **Graphs:** Nodes connected by edges.

Python built-in structures:

**List** - ordered collection.

```python
animals = ['cat', 'dog', 'mouse']
```

**Dictionary** - key/value mapping.

```python
car = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
```

## Lists

List operation costs:

| Operation | Example | Complexity | Why |
| --- | --- | --- | --- |
| **Append** | `cars.append("ford")` | `O(1)` average | Add at end. |
| **Index access** | `cars[2]` | `O(1)` | Direct index lookup. |
| **Delete middle** | `cars.pop(2)` | `O(n)` | Shift trailing elements. |
| **Search** | `cars.index("ford")` | `O(n)` | Scan until match. |

Lists struggle when:

1. Frequent middle deletions.
2. Frequent full-list searches.
