# Longest Common Subsequence

#### Description

Given two strings `text1` and `text2`, return the length of their longest common subsequence. The subsequence is not necessary a contigous range. It is different from a substring.

#### Example 1

Input: `text1 = "abcde", text2 = "ace"`

Output: `3`

Explanation: `ace` is the longest common subsequence.

#### Example 2

Input: `text1 = "abc", text2 = "abc"`

Output: `3`

#### Example 3

Input: `text1 = "abc", text2 = "def"`

Output: `0`

#### How to Solve

This is a typical dynamic programming problem. The easiest way is to create 2D array to save states up to indices i, j where i, j are index of each text. If text1[i] is the same as text2[j], the state will be matrix[i-1][j-1]+1. If not the same, take the maximum of matrix[i-1][j] and matrix[i][j-1]. The answer is in the bottom right of the matrix. For example, when `"abcdef"` and `"acbcf"` are given, the algorithm works as in below:

```
  | -   a   b   c   d   e   f
--+--------------------------
- | 0   0   0   0   0   0   0
a | 0   1   1   1   1   1   1
c | 0   1   1   2   2   2   2
b | 0   1   2   2   2   2   2
c | 0   1   1   3   3   3   3
f | 0   1   1   3   3   3   4   
```

The solution here uses two 1D auxiliary arrays instead of 2D matrix. This is a performance tweak. Allocating 1D array is much faster compared to 2D matrix even though it needs two arrays.

#### Solution
- Python

```python
class LCS:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        if len(text1) < len(text2):
            text1, text2 = text2, text1
        m, n = len(text1), len(text2)
        prev = [0 for _ in range(n+1)]
        for i in range(m):
            cur = [0 for _ in range(n+1)]
            for j in range(n):
                if text1[i] == text2[j]:
                    cur[j+1] = prev[j]+1
                else:
                    cur[j+1] = max(prev[j+1], cur[j])
            prev = cur
        return cur[-1]
```

#### Complexity
- Time: `O(mn)` -- m, n are lengths of given longer, shorter texts respectively
- Space: `O(n)`
