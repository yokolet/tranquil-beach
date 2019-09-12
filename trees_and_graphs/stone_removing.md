# Most Stones Removed with Same Row or Column

#### Description

Given an array of coordinates on the 2d plane which represents locations of stones, find the maximum number of stones can be removed if those are on the same rows or columns.

#### Example 1

Input: `stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]`

Output: `5`

Explanation: The 5 stones exist if rows and columns are expanded.

```
x  x  .
x  .  x
.  x  x
```

#### Example 2

Input: `stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]`

Output: `3`

Explanation: The maximum 3 stones exist if rows and columns are expanded.

```
x  .  x
.  x  .
x  .  x
```

#### Example 3

Input: `stones = [[0,0]]`

Output: `0`

Explanation: No other stone can be removed.

#### How to Solve

This question requires a bit of imagination what it is talking about.
The problem can be rephrased as the biggest island size where cells are
connected if the same row or column stones are there.

Given that, the union-find is an approach taken here.
As a preparation, stones' indices are saved in rows and cols dictionary.
The union is applied to rows and columns individually, but both shares the same group id list. While union is going on, it counts the number of stones at the same time.
When union is over for both rows and cols, the answer is there.

#### Solution

- Python

```python
from collections import defaultdict

class StoneRemoving:
    def removeStones(self, stones: 'List[List[int]]') -> int:
        n = len(stones)
        groups = [i for i in range(n)]
        rows = defaultdict(list)
        cols = defaultdict(list)

        def find(p):
            while p != groups[p]:
                p = groups[p]
            return p
        
        def union(m):
            count = 0
            for _, indices in m.items():
                parent = min(indices)
                x = find(parent)
                for idx in indices:
                    y = find(idx)
                    if x != y:
                        groups[y] = x
                        count += 1
            return count

        for i in range(n):
            r, c = stones[i]
            rows[r].append(i)
            cols[c].append(i)
        
        return union(rows) + union(cols)
```

#### Complexity

- Time: `O(nd)` -- n is a number of stones, d is a depth of union-find tree.
- Space: `O(n)`