# Edit Distance

#### Description

Given two words, find the minimum number of operations required to convert the first word to the second word.

To convert, following 3 operations are permitted:

- Insert a character
- Delete a character
- Replace a character

#### Example 1

Input: word1 = "horse", word2 = "ros"

Output: 3

Explanation:
```
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

#### Example 2

Input: word1 = "intention", word2 = "execution"

Output: 5

Explanation:
```
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

#### How to Solve

This is a typical Dynamic Programming problem.
Use 2 dimensional array(matrix) to save the status so far.

The first column and row is the distance compared to
0 length. Those will have values from 0 to m+1 and 0 to n+1
where m, n are the length of given words.

When two chars in the matrix are the same, copy the value of (i-1, j-1). If not, minimum of (i-1, j-1)+1, (i-1, j)+1,
(i, j-1)+1 will be the value.

The solution by DP is easy to understand, however, it is not so efficient. Another solution is by BFS(breadth first search).
Use a queue to save the processing so far. The value to save in the queue is a combination of rest of words and distance at that moment. When the rest of the words are the same, return the distance in the combination.
If not, shorten one char and plus one to distance, then
add to the queue. This has two patterns: one for the first word, another for the second word (insert or delete).
For replace, shorten both words by one and plus one to distance, then add to the queue.

#### Solution 1 -- DP

- Python

```python
class EditDistance:
    def minDistance(self, word1: str, word2: str) -> int:
        if not word1 or not word2:
            return max(len(word1), len(word2))
        m, n = len(word1), len(word2)
        memo = [[0 for j in range(n+1)] for i in range(m+1)]
        # intialize
        for i in range(m+1):
            memo[i][0] = i
        for i in range(n+1):
            memo[0][i] = i

        for i in range(1, m+1):
            for j in range(1, n+1):
                if word1[i-1] == word2[j-1]:
                    memo[i][j] = memo[i-1][j-1]
                else:
                    replace = memo[i-1][j-1]+1
                    insert = memo[i][j-1]+1
                    delete = memo[i-1][j]+1
                    memo[i][j] = min(replace, insert, delete)
        return memo[m][n]
```

#### Complexity 1

- Time: O(mn) -- where m, n are length of words
- Space: O(mn)

#### Solution 2 -- BFS

- Python

```python
from collections import deque

class EditDistance:
    def minDistance(self, word1: str, word2: str) -> int:
        seen = set()
        q = deque([(word1, word2, 0)])
        while q:
            (w1, w2, d) = q.popleft()
            if w1 == w2:
                return d
            if (w1, w2) in seen:
                continue
            else:
                seen.add((w1, w2))
            while w1 and w2 and w1[0] == w2[0]:
                w1 = w1[1:]
                w2 = w2[1:]
            q.append((w1, w2[1:], d + 1))       # remove
            q.append((w1[1:], w2, d + 1))       # insert
            q.append((w1[1:], w2[1:], d + 1))   # replace
```

#### Complexity 2

- Time: O(m + n)
- Space: O(m + n)