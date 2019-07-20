# Unique Paths with Obstacles to Cover All Squares

#### Description

Given m x n grid with obstacles on some squares, find how many unique paths from the starting to ending square are there. The paths must walk over all empty squares exactly once. Possible moves are either up, down, left or right. The obstacles prevent from going through.

Types of squares are:
- 1 -- start
- 2 -- end
- 0 -- empty
- -1 -- obstacle

#### Example 1

Input: 
```
[
    [1, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 2, -1]
]
```

Output: `2`

Explanation: possible paths are:
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)

#### Example 2

Input:
```
[
    [1, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 2]
]
```

Output: `4`

Explanation: possible paths are:
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)

#### Example 3

Input:
```
[
    [0, 1],
    [2, 0]
]
```

Output: `0`

#### How to Solve

The problem asks "a path in a graph that visits each vertex exactly once," which is called a Hamiltonian path (or traceable path). The Hamilitonian path problem can be solved by a backtracking.

The solution here uses DFS (Depth First Search).
After counting empty squares and finding the staring square, the code starts DFS with the position and count as the arguments. When it encounters the obstacle, 0 (no path) will be returned. When it comes the ending square, it returns 1 (one path found) if count is 0 (no path) otherwise returns 0.

The DFS goes by checking 4 squares. The return values from DFS are added up. In the end, all Hamiltonian paths will be counted.

#### Solution

- Python

```python
class UniquePathsObstaclesHam:
    def uniquePathsIII(self, grid: 'List[List[int]]') -> int:
        m, n = len(grid), len(grid[0])
        def findCountAndStart():
            count = 0
            for i in range(m):
                for j in range(n):
                    if grid[i][j] == 0: count += 1
                    if grid[i][j] == 1:
                        start = i, j
            return count, start

        def dsf(count, i, j):
            if i < 0 or j < 0 or i >= m or j >= n or grid[i][j] == -1:
                return 0
            if grid[i][j] == 2:
                return 1 if count == 0 else 0
            result = 0
            grid[i][j] = -1
            for nx, ny in [[0, -1], [-1, 0], [0, 1], [1, 0]]:
                result += dsf(count - 1, i + nx, j + ny)
            grid[i][j] = 0
            return result

        count, (start_i, start_j) = findCountAndStart()
        return dsf(count+1, start_i, start_j)
```

#### Complexity

- Time: O(mn) -- m, n are lengths of rows and cols
- Space: O(1)