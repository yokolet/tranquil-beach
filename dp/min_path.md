# Minimum Path Sum

#### Description

Given a `m x n` grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path. Possible moves are either down or right only.

#### Example
Input:

```
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
```

Output: `7`

Explanation: minimum path sum is: 1->3->1->1->1 = 7

#### How to Solve

A dynamic programmin (DP) approach works well for this kind of problems. Something different from a typical DP solution is that the problem doesn't need an auxiliary array. Directly updating the cell value doesn't conflict. While traversing cells, look at up and left cells. The current cell's value becomes minimum of those plus cell value. When all cells are traverssed, the bottom right cell has an answer.

#### Solution
- Python

```python
class MinPath:
    def minPathSum(self, grid: 'List[List[int]]') -> int:
        if not grid or not grid[0]: return 0
        m, n = len(grid), len(grid[0])
        for i in range(1, n):
            grid[0][i] += grid[0][i-1]
        for i in range(1, m):
            grid[i][0] += grid[i-1][0]
            for j in range(1, n):
                grid[i][j] += min(grid[i-1][j], grid[i][j-1])
        return grid[m-1][n-1]
```

#### Complaxity
- Time: `O(mn)` -- m, n are lengths of rows and columns of the grid
- Space: `O(1)`
