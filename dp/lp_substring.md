# Longest Palindromic Substring

#### Description

Given a string s, find the longest palindromic substring in s. 

The maximum length of s is 1000.

#### Example 1
Input: `"babad"`

Output: `"bab"` (or `"aba"`)

#### Example 2
Input: `"cbbd"`

Output: `"bb"`

#### How to Solve

This problem is normally categorized to the dynamic programming (DP). However, DP approach uses a 2 dimensional array, and its performance is O(n^2).

Instead of DP, this solution uses a sliding window approach. The window size is extended if the current window is a palindrome. The max window size, `max_len`, starts from 1. When extending the window, two patterns exist. A length of palindromic string is eithrt odd (such that "aba") or even (such that "bb"). To cover these two, substrings `s[i-max_len-1:i+1]` and `s[i-max_len:i+1]` are checked if those are palindrome or not. If it is a palindrome, make the window size bigger by adding 2 or 1 to `max_len`. Then, go to next index.


#### Solution
- Python

```python
class LongestPalindromicSubstring:
    def longestPalindrome(self, s: str) -> str:
        if not s: return ''
        max_len = 1
        start = 0
        for i in range(len(s)):
            if i - max_len >= 1 and\
                s[i-max_len-1:i+1] == s[i-max_len-1:i+1][::-1]:
                start = i - max_len - 1
                max_len += 2
            elif i - max_len >= 0 and\
                s[i-max_len:i+1] == s[i-max_len:i+1][::-1]:
                start = i - max_len
                max_len += 1
        return s[start:start+max_len]
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def length_of_lis(nums)
  return 0 if nums.nil? || nums.empty?
  memo = Array.new(nums.size, 0)
  max_length = 0
  nums.each do |v|
    left, right = 0, max_length
    while left < right
      mid = (left + right) / 2
      if memo[mid] < v
        left = mid + 1
      else
        right = mid
      end
    end
    memo[left] = v
    max_length = [max_length, left + 1].max
  end
  return max_length
end
```

#### Complexity
- Time: `O(n)` -- n is a length of a string
- Space: `O(1)`
