# Maximal Square

#### Description

Given a 2D binary matrix whose values are 0's and 1's, find the largest square containing only 1's and return its area.

#### Example
Input:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Output: `4`

Explanation: The shape should be a square. So, 2nd to 3rd rows and 3rd to 4th (or 4th to 5th) columns are biggest.

#### How to Solve

This is a typical DP problem. Use an auxiliary array to save the state so far. The state is a length of a side of the square. The auxiliary array is updated when the current cell value in the given matrix is '1'. Find the minimum value among upper left, upper and left cells. The auxiliary array value is the minimum plus one. Repeat all rows and columns starting from `(0, 0)`. The answer is in the last cell.

This solution uses the 1D auxiliary array to save memory. The previous state of upper left cell is saved in `prev` variable.

#### Solution
- Python

```python
class MaxSquare:
    def maximalSquare(self, matrix: 'List[List[str]]') -> int:
        if not matrix or not matrix[0]: return 0
        m, n = len(matrix), len(matrix[0])
        memo = [0 for _ in range(n+1)]
        max_sq, prev = 0, 0
        for i in range(1, m+1):
            for j in range(1, n+1):
                tmp = memo[j]
                if matrix[i-1][j-1] == '1':
                    memo[j] = min(memo[j-1], prev, memo[j]) + 1
                    max_sq = max(max_sq, memo[j])
                else:
                    memo[j] = 0
                prev = tmp
        return max_sq*max_sq
```

#### Complexity
- Time: `O(mn)` -- m,n are lengths of matrix's rows and cols
- Space: `O(n)`
