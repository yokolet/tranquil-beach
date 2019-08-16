# N-Queens

#### Description

Given in integer n, return all distinct solutions for the n-queens puzzle.

- Definition

    The n-queens puzzle is the problem to place n queens on an `n x n` chessboard. To avoid queens to battle each other, no two queens should be placed on the cells of horizontal and diagonal directions.

#### Example

Input: `4`

Output:

```
[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

'Q' and '.' represent a queen and empty space respectively.

#### How to Solve

The backtracking is an approach to solve this problem. Select a cell from the first row and check the horizontal and two diagonal cells. If other queens are not on those cells, move on to the next row and repeat the check. When all checks finish, the result is found for the first queen. Repeat whole set for the rest of queens.

This problem asks the all distinct solutions. To find all, the code doesn't return even though it reaches to the end state.

The second solution is streight forward and easy to understand, however, it runs slow. The time complexity is exponential. The first solution is an optimized solution using a set. Instead of checking all cells on horizontal and diagonals, it checks a number. When `n=4`, `r+c` and `r+n-1-c` gives numbers below. Each diagonal lines give the same number.

```
r + c         r+n-1-c
0 1 2 3       3 2 1 0
      ^       ^
1 2 3 4       4 3 2 1
    ^           ^
2 3 4 5       5 4 3 2
  ^               ^
3 4 5 6       6 5 4 3
^                   ^
```

If the number is in the set, other queens' precenses are quicky found.

#### Solution 1

- Python

```python
class Queens:
    def solveNQueens(self, n: int) -> 'List[List[str]]':
        rows, cols, diag_1, diag_2, = set(), set(), set(), set()
        queens, result = [], []

        def placeQueens():
            if len(queens) == n:
                # base case, all queens could be placed
                board = [['.' for i in range(n)] for j in range(n)]
                for r, c in enumerate(queens):
                    board[r][c] = 'Q'
                result.append([''.join(row) for row in board])

            # row r will be saved in index r
            r = len(queens)
            for c in range(n):
                if r not in rows and c not in cols and\
                    r+c not in diag_1 and r+n-1-c not in diag_2:
                    rows.add(r)
                    cols.add(c)
                    diag_1.add(r+c)
                    diag_2.add(r+n-1-c)
                    queens.append(c)
                    placeQueens()
                    queens.pop()
                    diag_2.remove(r+n-1-c)
                    diag_1.remove(r+c)
                    cols.remove(c)
                    rows.remove(r)
        placeQueens()
        return result
```

#### Solution 2

- Python

```python
class Queens:
    def solveNQueens(self, n: int) -> 'List[List[str]]':
        board = [['.' for _ in range(n)] for _ in range(n)]
        result = []

        def isValid(row, col):
            # check this row on the left
            for i in range(col):
                if board[row][i] == 'Q': return False
            # check upper diagonal
            for i, j in zip(range(row, -1 ,-1), range(col, -1, -1)):
                if board[i][j] == 'Q': return False
            # check lower diagonal
            for i, j in zip(range(row, n), range(col, -1, -1)):
                if board[i][j] == 'Q': return False
            return True

        def placeQueen(col):
            if col == n:
                # base case, all queens could be placed
                result.append([''.join(row) for row in board])
            for i in range(n):
                if isValid(i, col):
                    board[i][col] = 'Q'
                    placeQueen(col+1)
                    board[i][col] = '.'

        placeQueen(0)
        return result
```

#### Complexity

- Time: `O(n!)`
- Space: `O(n^2)`
