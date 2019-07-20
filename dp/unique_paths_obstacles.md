# Unique Paths with Obstacles

#### Description

Given m x n grid with obstacles on some squares, find how many unique paths from the top-left to bottom-right corner are there. Possible moves are either down or right. The obstacles prevent from going through.

#### Example

Input:
```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

Output: `2`

Explanation:

Because of the obstacle in the center, possible moves are
- Right -> Right -> Down -> Down
- Down -> Down -> Right -> Right

#### How to Solve

Dynamic Programming is an approach to solve this problem.
Like other typical Dynamic Programming solutions, the states so far are saved in the auxiliary array.

In this case, the initialization of auxiliary array can be done only the starting square. Since it comes to the obstacle square, the path becomes 0 at that position even in the first row and column. While going over all squares, the code updates each position by adding the value of up and left. The answer is in the last square.

The solution here uses 1 dimensional auxiliary array to save memory.

#### Solution

- Python

```python
class UniquePathsObstacles:
    def uniquePathsWithObstacles(self, obstacleGrid: 'List[List[int]]') -> int:
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        memo = [0 for _ in range(n)]
        if obstacleGrid[0][0] == 0: memo[0] = 1
        for i in range(m):
            if obstacleGrid[i][0]: memo[0] = 0
            for j in range(1, n):
                memo[j] = memo[j-1] + memo[j] if obstacleGrid[i][j] == 0 else 0
        return memo[-1]
```

#### Complexity

- Time: O(mn) -- m, n are lengths of rows and cols
- Space: O(n)
