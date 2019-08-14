# Snakes and Ladders

#### Description

Given an N x N board with the values of -1 or positive integer which represent a jumping position, find a minimum steps from a bottom left corner to the last cell. Depending on the N, the last cell is located on either upper left or upper right.

The board cells are numbered boustrophedonically, which means the number starts form the bottom left and alternating direction in each row. For example, N = 6:

```
36 35 34 33 32 31
25 26 27 28 29 30
24 23 22 21 20 19
13 14 15 16 17 18
12 11 10  9  8  7
 1  2  3  4  5  6
```

The next possible position is a current position plus 1 to 6 like a 6-sided die roll.

If the value in the board is not -1, the next position jumps forward (ladder) or backward (snake).

#### Example

Input:

```
[[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,-1,-1],
[-1,35,-1,-1,13,-1],
[-1,-1,-1,-1,-1,-1],
[-1,15,-1,-1,-1,-1]]
```

Output: `4`

Explanation: The shortest steps are:
1 (5, 0) -> 2 (5, 1) jump to 15 (3, 2) -> 17 (3, 3) jump to 13 (3, 0) -> 14 (3, 1) jump to 35 (0, 1) -> goal: 36 (0, 0)


#### How to Solve

Since this is a shortest path problem, BSF should work well. The tricky part is, the board is ordered boustrophedonically. The solution here calculates a row and column from the position. Another solution would expand the board to 1-d array.

Starting from the position 1 (row: n-1, col: 0), add a current position plus 1 to 6 to the queue as the next possible position. If the next position is a jumping point, updated the position. If a value popped out from the queue is the goal, the shortest path is found.

#### Solution

- Python

```python
class SnakesLadders:
    def snakesAndLadders(self, board: 'List[List[int]]') -> int:
        n = len(board)
        goal = n * n
        def findRowCol(pos):
            q, r = divmod(pos-1, n)
            if q % 2 == 0:
                return n - 1 - q, r
            else:
                return n - 1 - q, n - 1 - r
    
        queue = [(1, 0)]
        visited = set([1])
        while queue:
            pos, step = queue.pop(0)
            r, c = findRowCol(pos)
            if board[r][c] != -1: pos = board[r][c]
            if pos == goal: return step
            for i in range(1, 7):
                tmp = pos + i
                if tmp <= goal and tmp not in visited:
                    visited.add(tmp)
                    queue.append((tmp, step + 1))
        return -1
```

#### Complexity

- Time: `O(n)`
- Space: `O(n)`