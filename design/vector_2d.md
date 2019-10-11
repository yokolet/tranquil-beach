# Flatten 2D Vector

#### Description

Design an iterator to flatten a 2d vector. It should support `next` and `hasNext` operations.

#### Example
```python
iterator = Vector2D([[1,2],[3],[4]])

iterator.next()       # return 1
iterator.next()       # return 2
iterator.next()       # return 3
iterator.hasNext()    # return True
iterator.hasNext()    # return True
iterator.next()       # return 4
iterator.hasNext()    # return False
```

#### How to Solve

Since the source is 2D vector, flatten it in the constructor. To avoid pointer management, reverse the flattened array and use `pop` method to take values out one by one. When `next` method is called, pop the value. When `hasNext` method is called, check the length of flattened array.

#### Solution
- Python

```python
class Vector2D:
    def __init__(self, v: 'List[List[int]]'):
        self.values = [j for i in v for j in i][::-1]

    def next(self) -> int:
        return self.values.pop()

    def hasNext(self) -> bool:
        return len(self.values) > 0
```

#### Complexity
- Time: constructor: `O(mn)`, `next`: `O(1)`, `hasNext`: `O(1)` -- m,n are the lengths of outer and inner vectors respectively
- Space: `O(mn)`
