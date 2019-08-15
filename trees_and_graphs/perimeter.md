# Island Perimeter

#### Description

Given a two-dimensional array of 0 (water) and 1 (land), find the perimeter of the island.

- Definition

    The island cells are connected horizontally and vertically (not diagonally). Outside of the grid is all water. Only one island exists which doesn't have any lake. Each cell is a square with side length 1.

#### Example

Input:

```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]
```

Output: `16`

Explanation:

```
 _ _ _ _
| |x| | |
 _ _ _ _
|x|x|x| |
 _ _ _ _
| |x| | |
 _ _ _ _
|x|x| | |
 _ _ _ _
```

The perimeter is all bars around X, but not shared by Xs.

#### How to Solve

Go over all cells from upper left to bottom right. When the grid value is 1 (land), add 4 to the result anyway. After the second row and the second column, check the cells above and left. If those are the land, subtract 2 respectively. These 2 are shared edges by two land cells, so should not be counted.

#### Solution

- Python

```python
class Perimeter:
    def islandPerimeter(self, grid: 'List[List[int]]') -> int:
        result, m, n = 0, len(grid), len(grid[0])
        for r in range(m):
            for c in range(n):
                if grid[r][c] == 1:
                    result += 4
                    if r > 0 and grid[r-1][c] == 1:
                        result -= 2
                    if c > 0 and grid[r][c-1] == 1:
                        result -= 2
        return result
```

#### Complxity

- Time: `O(m*n)` -- m, n are the length of rows an cols of the given grid
- Space: `O(1)`