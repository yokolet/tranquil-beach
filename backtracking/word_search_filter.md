# Multiple Words Search

#### Description

Given a two dimensional array of letters and a list of words, find whether the words exist in the 2D array or not. The letters in each word can be searched from the starting cell to up, left, right, or down cell. The same letter cell may not be used more than once. 

All letters in the words are lowercase, a-z. The words in the given list are distinct.

#### Example

Input: `words = ["oath","pea","eat","rain"]`

```
board = [
    ['o','a','a','n'],
    ['e','t','a','e'],
    ['i','h','k','r'],
    ['i','f','l','v']
]
```

Output: `["eat","oath"]`

#### How to Solve

The depth first search (DFS) is a good approach to go deeper to find the word. However, this needs backtracking as well. When one of the same letters used to go deeper, and later, adjacent another same letter may be used for a different index in the given word. Not only marking as visited, but also making it back to original is needed. For this reason, the solution here uses the backtracking.

Additionally, the solution uses Trie not to iterate the same search for each word. Starting from every row and column with an empty string, the dfs extends the string, character by character looking at nodes in Trie. While running the dfs multiple times, the same word may be found more than once. This is solved by using a set.

#### Solution

- Python

```python
class WordSearchFilter:
    def findWords(self, board: 'List[List[str]]', words: 'List[str]') -> 'List[str]':
        m, n = len(board), len(board[0])
        result = set()
        def buildTrie():
            root = {}
            for word in words:
                cur = root
                for c in word:
                    if c not in cur:
                        cur[c] = {}
                    cur = cur[c]
                cur['$'] = {} # a word exists at cur node
            return root

        def dfs(i, j, w, cur):
            if '$' in cur: result.add(w)
            if i < 0 or i == m or j < 0 or j == n: return
            if board[i][j] not in cur: return
            c = board[i][j]
            board[i][j] = '#'
            dfs(i-1, j, w+c, cur[c])
            dfs(i+1, j, w+c, cur[c])
            dfs(i, j-1, w+c, cur[c])
            dfs(i, j+1, w+c, cur[c])
            board[i][j] = c
        
        root = buildTrie()
        for i in range(m):
            for j in range(n):
                dfs(i, j, '', root)
        return list(result)
```

#### Complexity

- Time: `O(m * n * 4^l)` -- m, n, l are lengths of rows, columns, and each word respectively
- Space: `O(k * l)` -- k, l are lengths of word list and each word respectively