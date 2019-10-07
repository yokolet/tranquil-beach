# Maximal Square

#### Description

#### Example

#### How to Solve

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
- Time:
- Space: