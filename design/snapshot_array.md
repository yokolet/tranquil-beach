# Snapshot Array

#### Description

Design a `SnapshotArray` class that supports methods below:
- `SnapshotArray(length: int)`: constructor. initializes an array-like data structure with the given length. Initially, each element has a value, 0.
- `set(index, val) -> None`: sets the value, `val`, at the given `index`.
- `snap() -> int`: takes a snapshot of the array and returns the `snap_id`, which is the total number of times `snap()` method is called minus 1.
- `get(index, snap_id) -> int`: returns the value at the given `index` of snapshot whose id is `snap_id`.

#### Example

Input: `["SnapshotArray","set","snap","set","get"]`, `[[3],[0,5],[],[0,6],[0,0]]`

Output: `[null,null,0,null,5]`

Explanation:
```
sa = SanpshotArray(3)
sa.set(0, 5)
sa.snap() # -> 0
sa.set(0, 6)
sa.get(0, 0) # -> 5
```

#### How to Solve

The implementation itself is easy to think of. However, this problem asks how fast the implementation runs. If the implementation creates an array of given length and makes deep copy of the array at each snap method call, it will get time limit exceeded error. To make it run faster, not to make whole lot of array(s) is the key. The solution here uses dictionaries to save values for both current and snapshot. If the key doesn't exist, the value is 0.

#### Solution
- Python

```python
class SnapshotArray:
    def __init__(self, length: int):
        self.length = length
        self.values = {}
        self.snapshot = []

    def set(self, index: int, val: int) -> None:
        self.values[index] = val

    def snap(self) -> int:
        s = {}
        for k, v in self.values.items():
            s[k]=v
        self.snapshot.append(s)
        return len(self.snapshot) - 1

    def get(self, index: int, snap_id: int) -> int:
        s = self.snapshot[snap_id]
        if index in s:
            return s[index]
        else:
            return 0
```

#### Complexity
- Time: `O(1): constructor, set, get`, `O(n): snap` -- n is a number of `set` calls
- Space: `O(n*m)` -- m is a number of `snap` calls
