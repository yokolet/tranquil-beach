# Word Break

#### Description

Given a non-empty string `s` and a dictionary `wordDict` which is a list of non-empty words, determine `s` can be segmented into a spce-separated sequence of one or more words in dictionary.

#### Example 1
Input: `s = 'leetcode', wordDict = ['leet', 'code']`

Output: `True`

Explanation: `'leetcode' = 'leet' + 'code'`

#### Example 2
Input: `s = 'applepenapple', wordDict = ['apple', 'pen']`

Output: `True`

Explanation: `'applepenapple' = 'apple' + 'pen' + 'apple'`

#### Example 3
Input: `s = 'catsandog', wordDict = ['cats', 'dog', 'sand', 'and', 'cat']`

Output: `False`

#### How to Solve

A DP approach is taken here. The auxiliary array is created with the False values. The array saves the state whether characters between `j` to `i` exists as a word in `wordDict` and previously the word exists in the `wordDict` ending at the index `j`. Iterate over the given string while extending the length one by one. In the end, the last index of the auxiliary array has the answer.

#### Solution
- Python

```python
class WordBreak:
    def wordBreak(self, s: str, wordDict: 'List[str]') -> bool:
        n, dict = len(s), set(wordDict)
        memo = [False for _ in range(n+1)]
        memo[0] = True
        for i in range(1, n+1):
            for j in range(i):
                if memo[j] and s[j:i] in dict:
                    memo[i] = True
                    break
        return memo[n]
```

#### Complexity
- Time: `O(n^2)` -- n is a length if the given string
- Space: `O(n)`
