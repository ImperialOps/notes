# Python :material-language-python:

## Python Data Structures Cheat Sheet

| Type      | Syntax   | Ordered | Mutable | Unique Only | Search/Fetch | Complexity |
| :-------- | :------- | :-----: | :-----: | :---------: | :----------- | :--------- |
| **List**  | `[...]`  |   ✅    |   ✅    |     ❌      | By Index     | **O(1)**   |
|           |          |         |         |             | By Value     | **O(n)**   |
| **Tuple** | `(...)`  |   ✅    |   ❌    |     ❌      | By Index     | **O(1)**   |
| **Set**   | `{...}`  |   ❌    |   ✅    |     ✅      | By Value     | **O(1)**   |
| **Dict**  | `{k: v}` |  ✅\*   |   ✅    |  Keys: ✅   | By Key       | **O(1)**   |

---

### Core Concepts

- **The "Hash" Advantage:** Sets and Dictionaries use a Hash Table. This is why searching for a value in a Set with 1 million items is just as fast as searching in a Set with 10 items (**O(1)**).
- **The List Penalty:** Searching for a value in a List requires Python to look at every single item one by one (**O(n)**). As your list grows, your code slows down.
- **Immutability:** A Tuple is the only one in this list that cannot be changed after creation. This makes it "Hashable" and safe to use as a Dictionary key.
- **Dict Ordering:** Since Python 3.7, Dictionaries remember the order in which you added items, but they are still optimized for key-based lookups, not index-based lookups.

### Example of Set of Tuples

```python
# A set of (x, y) coordinates
visited_spots = {(0, 0), (1, 5), (10, 20)}

# Even if this set had 10 million tuples, 
# this check is O(1)
if (10, 20) in visited_spots:
    print("Found it!")
```

