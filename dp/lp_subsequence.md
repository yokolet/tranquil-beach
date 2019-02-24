# Longest Palindromic Subsequence

#### Description

Given a string s, find the longest palindromic subsequence's length in s.

The maximum length of s is 1000.

#### Example 1
Input: `"bbbab"`

Output: 4

Explanation: `"bbbb"` is the longest palindromic subsequence.

#### Example 2
Input: `"cbbd"`

Output: 2

Explanation: `"bb"` is the longest palindromic subsequence.

#### How to Solve

Go over all characters one by one.
While iterating, make substring length longer one by one.
Save the length of palindrome to an auxiliary array as a state.
Using the auxiliary array as previous state, update the length.

If 2 dimensional array is used, it is easy to understand. However, it runs very slow. This solution uses 2 independent arrays to keep previous and ongoing states.

#### Solution
- Python

```python
class LongestPalindromicSubsequence:
    def longestPalindromeSubseq(self, s: str) -> int:
        n = len(s)
        if s == s[::-1]: return n
        prev = [0] * n
        for i in range(n-1, -1, -1):
            cur = [0] * n
            cur[i] = 1
            for l in range(i+1, n):
                if s[i] == s[l]:
                    cur[l] = prev[l-1] + 2
                else:
                    cur[l] = max(prev[l], cur[l-1])
            prev = cur
        return prev[-1]
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def longest_palindrome_subseq(s)
  n = s.size
  return n if s == s.reverse
  prev = Array.new(n, 0)
  (n-1).downto(0) do |i|
    cur = Array.new(n, 0)
    cur[i] = 1
    (i+1...n).each do |l|
      if s[i] == s[l]
        cur[l] = prev[l - 1] + 2
      else
        cur[l] = [prev[l], cur[l-1]].max
      end
    end
    prev = cur
  end
  prev[-1]
end
```

#### Complexity
- Time: O(n^2)
- Space: O(n)