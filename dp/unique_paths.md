# Unique Paths

#### Description

Given m x n grid, find how many unique paths from the top-left to bottom-right corner are there. Possible moves are either down or right.

- m and n will be at most 100.

#### Example 1

Input: `m = 3, n = 2`

Output: `3`

Explanation: possible three ways are:

- right -> right -> down
- right -> down -> right
- down -> right -> right

#### Example 2

Input: m = 7, n = 2

Output: 28

#### How to Solve

Dynamic Programming is an approach to solve this problem.
Like other typical Dynamic Programming solutions, the states so far are saved in the auxiliary array.

In this case, the code initializes first row and column to 1, which means only one way is possible to reach there.
Then, the code updates each square by adding the value of up and left. The answer is in the last square.

The solution 1 here is a naive approach by 2 dimensional auxiliary array. This works well, still. However, the second solution is effective. The solution 2 uses 1 dimensional auxiliary array. The time complexity is the same, but the space complexity is smaller.

#### Solution 1

- Python

```python
class UniquePaths:
    def uniquePaths(self, m: int, n: int) -> int:
        memo = [[0 for _ in range(n)] for _ in range(m)]
        for i in range(m):
            memo[i][0] = 1
        for i in range(n):
            memo[0][i] = 1
        for i in range(1, m):
            for j in range(1, n):
                memo[i][j] = memo[i-1][j] + memo[i][j-1]
        return memo[m-1][n-1]
```

#### Complexity 1

- Time: O(mn)
- Space: O(mn)

#### Solution 2

- Python

```python
class UniquePaths:
    def uniquePaths(self, m: int, n: int) -> int:
        memo = [1 for _ in range(n)]
        for i in range(1, m):
            for j in range(1, n):
                memo[j] += memo[j-1]
        return memo[-1]
```

#### Complexity 2

- Time: O(mn)
- Space: O(n)