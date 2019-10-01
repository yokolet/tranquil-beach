# Longest Substring with At Most Two Distinct Characters

#### Description

Given a string, find the length of the longest substring that contains at most 2 distinct characters.

#### Example 1
Input: `'eceba'`

Output: `3`

Explanation: `'ece'` is the longest

#### Example 2
Input: `'ccaabbb'`

Output: `5`

Explanation: `'aabbb'` is the longest

#### How to Solve

The solution saves the last occurence of each character in a dictionary, `memo`. When the size of the `memo` exceeds 2, find the min index in the `memo` as the left pointer. Not to recount the min index char, delete it from the `memo`. Then, compare max_length.

Similar problems:
- [Fruit Into Baskdets](fruit_baskets.md)
- [Longest Substring With At Most K Distinct Characters](longest_substring_k_distinct.md)

#### Solution

- Python

```python
class LongestSubstring2Distinct:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        left, max_len, memo = 0, 0, {}
        for i, c in enumerate(s):
            memo[c] = i
            if len(memo) > 2:
                left = min(memo.values())
                del memo[s[left]]
                left += 1
            max_len = max(max_len, i-left+1)
        return max_len
```

#### Complexity
- Time: `O(n)` -- n is a length of the given string
- Space: `O(n)`