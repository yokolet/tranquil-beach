# Candy Crush

#### Description

Given a 2D positive integer array, `board`, which represents the grid of candy, implement a basic elimination algorithm of candy crush.
The values in the `board` represent the types of candies. If the value is zero, the cell is empty. The `board` goes to the stable state (final state) by crushing candies based on the rules below. Once the `board` becomes stable, return the final state of the `board`.

- Rules
    1. If three or more candies of the same type are adjacent vertically or horizontally, crush all of those at the same time.
    2. After crushing the candies, existing candies drops a number of crushed candies of that column.
    3. Repeat 1 and 2 until no more candies can be crushed.

#### Example

Input:
```
board =
[
    [110,5,112,113,114],
    [210,211,5,213,214],
    [310,311,3,313,314],
    [410,411,412,5,414],
    [5,1,512,3,3],
    [610,4,1,613,614],
    [710,1,2,713,714],
    [810,1,2,1,1],
    [1,1,2,2,2],
    [4,1,4,4,1014]
]
```

Output:
```
[
    [0,0,0,0,0],
    [0,0,0,0,0],
    [0,0,0,0,0],
    [110,0,0,0,114],
    [210,0,0,0,214],
    [310,0,0,113,314],
    [410,0,0,213,414],
    [610,211,112,313,614],
    [710,311,412,613,714],
    [810,411,512,713,1014]
]
```

Explanation:
```
initial state          after the first crushes    stable state
110  5  112 113 114      110  0   0   0   0        0   0   0   0   0 
210 211  5  213 214      210  0   0  113 114       0   0   0   0   0
310 311  3  313 314      310  0   0  213 214       0   0   0   0   0
410 411 412  5  414      410  0  112 313 314      110  0   0   0  114
 5   1  512  3   3        5   5   5   5  414      210  0   0   0  214
610  4   1  613 614      610 211  3   3   3       310  0   0  113 314
710  1   2  713 714      710 311 412 613 614      410  0   0  213 414
810  1   2   1   1       810 411 512 713 714      610 211 112 313 614
 1   1   2   2   2        1   1   1   1   1       710 311 412 613 714
 4   1   4   4  1014      4   4   4   4  1014     810 411 512 713 1014
```

#### How to Solve

This problem requires exhaustive searchs starting from all cells followed by the board update, similar to the [Game of Life](game_of_life.md). While searching the cells to match criteria, it's possible to count the same cell multipl times. For this reason, checked cells are saved in the array of sets. This array will have crushed rows in each column. When the board is updated, as many as zeroes to the same number of crushed rows of the column are added at the top. If the cell is not among crushed, copy it to the updated board.

#### Solution
- Python

```python
class CandyCrush:
    def candyCrush(self, board: 'List[List[int]]') -> 'List[List[int]]':
        def search(b, row, col):
            # down
            if row < rows-2 and b[row+1][col] == b[row][col] and b[row+2][col] == b[row][col]:
                counts[col].add(row)
                counts[col].add(row+1)
                counts[col].add(row+2)
                i = row + 3
                while i < rows and b[i][col] == b[row][col]:
                    counts[col].add(i)
                    i += 1          
            # right
            if col < cols-2 and b[row][col+1] == b[row][col] and b[row][col+2] == b[row][col]:
                counts[col].add(row)
                counts[col+1].add(row)
                counts[col+2].add(row)
                j = col + 3
                while j < cols and b[row][j] == b[row][col]:
                    counts[j].add(row)
                    j += 1
        
        def update():
            for c in range(cols):
                i = rows-1
                for r in range(rows-1, -1, -1):
                    if r not in counts[c]:
                        board[i][c] = board[r][c]
                        i -= 1
                while i >= 0:
                    board[i][c] = 0
                    i -= 1

        rows, cols= len(board), len(board[0])
        while True:
            counts = [set() for _ in range(cols)]
            for r in range(rows):
                for c in range(cols):
                    if board[r][c] == 0: continue
                    search(board, r, c)
            if sum([len(c) for c in counts]) == 0: break
            update()
        return board
```

#### Complexity
- Time: `O((mn)^2)` -- m,n are lengths of rows and columns respectively
- Space: `O(n)`
