# Longest Common Prefix

#### Description

Given an array of strings, find the longest common prefix. If there is no common prefix, return an empty string.

#### Example 1
Input: `['flower','flow','flight']`

Output: `'fl'`

#### Example 2
Input: `['dog','racecar','car']`

Output; `''`

#### How to Solve

Since a common prefix is no longer than the minimum length string, find that for the first step. It is an initial prefix. The next step is to find how many strings have the prefix. If the count is not the same as the given array, cut the last character from the prefix. Repeat counting and cutting. When all strings have the prefix, the answer is found.

#### Solution
- Python

```python
class LongestPrefix:
    def longestCommonPrefix(self, strs: 'List[str]') -> str:
        if not strs: return ''
        n = len(strs)
        prefix = min(strs, key=len)
        while prefix and sum([w[:len(prefix)]==prefix for w in strs]) != n:
            prefix = prefix[:-1]
        return prefix
```

#### Complexity
- Time: `O(m+n)` -- m,n are lengths of given array and prefix
- Space: `O(1)`
