# Word Break

#### Description

#### Example 1

#### Example 2

#### Example 3

#### How to Solve

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
- Time:
- Space: