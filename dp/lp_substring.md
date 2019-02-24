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

This problem is normally categorized to dynamic programming (DP).
The solution by DP is one. However, DP approach uses a 2 dimensional array, and its performance is O(n^2).

Instead of DP, this solution uses a sliding window approach.
A length of palindromic string is odd (such that "aba") or even (such that "bb"). For both length, check the substring is
palindrome or not. If it is a palindrome, make window size bigger. Then, go to next index. 


#### Solution
- Python

```python
class LongestPalindromicSubstring:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s: return ""
        max_length = 1
        start = 0
        for i in range(1, len(s)):
            if i - max_length >= 1 and\
                s[i-max_length-1:i+1] == s[i-max_length-1:i+1][::-1]:
                start = i - max_length - 1
                max_length += 2
            elif i - max_length >= 0 and\
                s[i-max_length:i+1] == s[i-max_length:i+1][::-1]:
                start = i - max_length
                max_length += 1
        return s[start:start+max_length]
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
- Time: O(n)
- Space: O(1)