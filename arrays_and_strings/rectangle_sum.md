# Max Sum of Rectangle No Larger Than K

#### Description

Given a non-empty 2D metrix and an integer `k`, find the max sum of a rextangle in the matrix such that its sum is no larger than k.

#### Example

Input: `matrix = [[1,0,1],[0,-2,3]], k = 2`

Output: `2`

Explanation: The sum of rectangle `[[0,1],[-2,3]]` is 2 which is the max sum no larger than `k (k=2)`.

#### How to Solve

A couple of approaches exist for this problem for example, using prefix sum or binary search tree. Among those, the solution here took prefix sum and binary search combination.

The problem asks "no larger than k" instead of equals to k. So, the prefix sum should be saved in a sorted order to find the value less than preifx sum - k. Use binary search to find such value exists. If it does, compare and update max value. The prefix sum should be always added in to the sorted array.

#### Solution
- Python

```python
import bisect

class RectangleSum:
    def maxSumSubmatrix(self, matrix: 'List[List[int]]', k: int) -> int:
        m, n = len(matrix), len(matrix[0])
        max_sum = float('-inf')
        for i in range(m):
            for j in range(1, n):
                matrix[i][j] += matrix[i][j-1]
        for c1 in range(n):
            for c2 in range(c1, n):
                acc, memo = 0, [0]
                for r in range(m):
                    v = matrix[r][c1-1] if c1 > 0 else 0
                    acc += matrix[r][c2] - v
                    idx = bisect.bisect_left(memo, acc-k)
                    if idx < len(memo):
                        max_sum = max(max_sum, acc-memo[idx])
                    bisect.insort_left(memo, acc)
        return max_sum
```

#### Complexity
- Time: `O(n^2*mlong(m))` -- m, n are lengths of cols and rows respectively
- Space: `O(m)`
