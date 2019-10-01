# Longest Substring With At Most K Distinct Characters

#### Description

Given a string, find the length of the longest substring that contains at most k distinct characters.

#### Example 1

Input: `s = 'eceba, k = 2`

Output: `3`

Explanation: `ece` is the longest substring with 2 distinct characters.

#### Example 2

Input: `s = 'aa', k = 1`

Output: `2`

Explanation: `'aa'` is the longest (sub)string with 1 distinct characters.

#### How to Solve

The solution saves the last occurence of each character in a dictionary, `memo`. When the size of the `memo` exceeds the given k, find the min index in the `memo` as the left pointer. Not to recount the min index char, delete it from the `memo`. Then, compare max_length.

Similar problems:
- [Fruit Into Baskdets](fruit_baskets.md)
- [Longest Substring With At Most 2 Distinct Characters](longest_substring_2_distinct.md)

#### Solution

- Python

```python
class LongestSubstringKDistinct:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        left, max_len, memo = 0, 0, {}
        for i, char in enumerate(s):
            memo[char] = i
            if len(memo) > k:
                left = min(memo.values())
                del memo[s[left]]
                left += 1
            max_len = max(max_len, i-left+1)
        return max_len
```

#### Complexity

- Time: `O(n)` -- n is a length of the given string
- Space: `O(n)`