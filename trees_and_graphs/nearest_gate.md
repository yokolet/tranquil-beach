# Walls and Gates

#### Description

Given `m x n` grid with three types of values below, fill each empty room with the distace to its nearest gate. It it's impossible to reach to any gate, leave the value, INF, as is.

- Definition
    -  -1: a wall or obstacle
    -   0: a gate
    - INF: empty room, 2^31-1 (2147483647)

#### Example

Input:

```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```

Output:

```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

#### How to Solve

This is an all source shortest path problem. Start from all gates, expand its reach to four directions. Compare current cell value to previous cell value + 1, and take smaller one as the current cell value.

Naive two dimensional grid search runs slow. The approach here is basically same as the naive solution. However, instead of looping all four direction and expanding those, the four directions with distance are added to the queue. When the distance from the queue is smaller, next four directions are added. 


#### Solution

- Python

```python
class NearestGate:
    def wallsAndGates(self, rooms: 'List[List[int]]') -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        if not rooms or not rooms[0]: return
        m, n = len(rooms), len(rooms[0])

        def bfs(row, col):
            queue = [
                (row-1, col, 1),
                (row, col-1, 1),
                (row, col+1, 1),
                (row+1, col, 1)
            ]
            while queue:
                r, c, v = queue.pop(0)
                if 0 <= r < m and 0 <= c < n and rooms[r][c] > v:
                    rooms[r][c] = v
                    queue.append((r-1, c, v+1))
                    queue.append((r, c-1, v+1))
                    queue.append((r, c+1, v+1))
                    queue.append((r+1, c, v+1))

        for row in range(m):
            for col in range(n):
                if rooms[row][col] != 0: continue
                bfs(row, col)
```

#### Complexity

- Time: `O(n^3)` -- n is either rows or cols, bigger one
- Space: `O(m*n)` 