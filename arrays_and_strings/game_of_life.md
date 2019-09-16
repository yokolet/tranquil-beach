# Game of Life

#### Description

Given a board with m by n cells, compute the next state of the board after one update following the rule below. 

- Each cell has an initial state live (1) or dead (0).
- Each cell interacts with its eight neighbors (horizontal, vertical, diagonal).
- Case 1: Any live cell with fewer than two live neighbors dies, as if caused by under-population.
- Case 2: Any live cell with two or three live neighbors lives on to the next generation.
- Case 3: Any live cell with more than three live neighbors dies, as if by over-population.
- Case 4: Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
- The next state is created by applying the 4 cases simultaneously.

#### Example
Input:

```
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
```

Output:

```
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```

#### How to Solve

All cells should be updated looking at 8 cells surrounded. The time complexity remains in O(m*n), while the space complexity can be improved to O(1).

The idea is to use 2 and 3 for next state. To calculate how many neighbors are alive, `x & 1` will be used. So, `2 & 1 = 0, 3 & 1 = 1` will be used to calculation. In the end, board values are switched to `x >> 1`. The final board values are 0 and 1 only.

#### Solution
- Python

```python
class GameOfLife:
    def gameOfLife(self, board: 'List[List[int]]') -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        m, n = len(board), len(board[0])

        def calc(i, j):
            neighbors = [
                [i-1, j-1],[i-1,j],[i-1,j+1],
                [i, j-1],[i,j+1],
                [i+1, j-1],[i+1, j],[i+1,j+1]
            ]
            sum = 0
            for r,c in neighbors:
                if 0 <= r < m and 0 <= c < n:
                    sum += (board[r][c] & 1)
            return sum

        for i in range(m):
            for j in range(n):
                status = calc(i, j)
                if board[i][j] == 1 and (status == 2 or status == 3):
                    board[i][j] = 3
                else:
                    if status == 3:
                        board[i][j] = 2
        for i in range(m):
            for j in range(n):
                board[i][j] >>= 1
```

- Ruby

```ruby
# @param {Integer[][]} board
# @return {Void} Do not return anything, modify board in-place instead.
def game_of_life(board)
  m = board.size
  n = board[0].size
  calc =-> (i, j) {
    neighbors = [
        [i-1, j-1], [i-1, j], [i-1, j+1],
        [i, j-1], [i, j+1],
        [i+1, j-1], [i+1, j], [i+1, j+1]
    ]
    sum = 0
    neighbors.each do |neighbor|
      r, c = neighbor[0], neighbor[1]
      if 0 <= r && r < m && 0 <= c && c < n
        sum += (board[r][c] & 1)
      end
    end
    sum
  }
  m.times do |i|
    n.times do |j|
      status = calc.call(i, j)
      if board[i][j] == 1 && (status == 2 || status == 3)
        board[i][j] = 3
      else
        if status == 3
          board[i][j] = 2
        end
      end
    end
  end
  m.times do |i|
    n.times do |j|
      board[i][j] >>= 1
    end
  end
end
```

#### Complexity
- Time: `O(mn)` -- board size is m rows and n cols
- Space: `O(1)`
