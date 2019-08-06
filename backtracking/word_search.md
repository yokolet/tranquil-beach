# Word Search

#### Description

Given a two dimensional array of letters and a word, find whether the word exists in the 2D array or not. The letters in the word can be searched from the starting cell to up, left, right, or down cell. The same letter cell may not be used more than once. 

#### Example 1

Input: `word = 'ABCCED'`

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```

Output: `True`

#### Example 2

Input: `word = 'ABCB'

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```

Output: `False`

#### Example 3

Input: `word = 'ABCESEEEFS'

```
board =
[
  ['A','B','C','E'],
  ['S','F','E','S'],
  ['A','D','E','E']
]
```

Output: `True`

#### How to Solve

The depth first search (DFS) is a good approach to go deeper to find the word. However, this needs backtracking as well. When one of the same letters used to go deeper, and later, adjacent another same letter may be used for a different index in the given word. Not only marking as visited, but also making it back to original is needed. For this reason, the solution here uses the backtracking.

#### Solution

- Python

```python
class WordSearch:
    def exist(self, board: 'List[List[str]]', word: str) -> bool:
        m, n = len(board), len(board[0])
        def dfs(i, j, w):
            if not w: return True
            cur = board[i][j]
            board[i][j] = '#'
            if (i > 0 and board[i-1][j] == w[0] and dfs(i-1, j, w[1:])) \
                or (i < m-1 and board[i+1][j] == w[0] and dfs(i+1, j, w[1:])) \
                or (j > 0 and board[i][j-1] == w[0] and dfs(i, j-1, w[1:])) \
                or (j < n-1 and board[i][j+1] == w[0] and dfs(i, j+1, w[1:])):
                return True
            board[i][j] = cur

        for i in range(m):
            for j in range(n):
                if board[i][j] == word[0] and dfs(i, j, word[1:]):
                    return True
        return False
```

#### Complexity

- Time: `O(4^l)` -- l is a length of the given word
- Space: `O(1)`