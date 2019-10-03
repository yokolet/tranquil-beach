# Longest Increasing Path in a Matrix

#### Desciption

Given a 2-d matrix of integers, find the length of the longest increasing path. The path only goes up, down, left or right cells and should not move to outside of the boundary.

#### Example 1
Input:

```
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
```

Output: `4`

Explanation: The longest increasing path is `[1, 2, 6, 9]`.

#### Example 2
Input:

```
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
```

Output: `4`

Explanation: The longest increasing path is `[3, 4, 5, 6]`

#### How to Solve

The problem asks a strictly increasing path. This means to find the DAG (directed acyclic graph). The easiest way to find such path is a depth first search (DFS). Starting from each row/col, repeat finding next cells where the values are less than the current cell value. Alternatively, the value can be greater. Both find the same paths.

The naive DFS approach runs slow. The solution here uses the memoization to make it run faster. Save the maximum path length at each row/col to the auxiliary 2-d array. If the path length at the cell is calculated before, returns the saved value. This cuts down the repetition of calculating the same paths.

#### Solution
- Python

```python
class LongestPath:
    def longestIncreasingPath(self, matrix: 'List[List[int]]') -> int:
        if not matrix or not matrix[0]: return 0
        n, m = len(matrix), len(matrix[0])
        memo = [[-1 for _ in range(m)] for _ in range(n)]

        def dfs(r, c):
            if memo[r][c] != -1: return memo[r][c]
            max_p = 0
            for i,j in [(r-1, c), (r, c-1), (r, c+1), (r+1, c)]:
                if 0 <= i < n and 0 <= j < m and matrix[r][c] > matrix[i][j]:
                    max_p = max(max_p, dfs(i, j))
            memo[r][c] = max_p + 1
            return memo[r][c]

        max_path = 0
        for r in range(n):
            for c in range(m):
                max_path = max(max_path, dfs(r, c))
        return max_path
```

#### Complexity
- Time: `O(n*m)` -- n, m are length of matrix's rows and columns.
- Space: `O(n*m)`
