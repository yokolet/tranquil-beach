# Longest Palindromic Subsequence

#### Description

Given a string `s`, find the length of the longest palindromic subsequence.

The maximum length of `s` is 1000.

#### Example 1
Input: `"bbbab"`

Output: `4`

Explanation: `"bbbb"` is the longest palindromic subsequence.

#### Example 2
Input: `"cbbd"`

Output: `2`

Explanation: `"bb"` is the longest palindromic subsequence.

#### How to Solve

The dynamic programming is the approach taken here.
The solution uses two 1D auxiliary arrays rather than 2D array. It helps to reduce a space complexity. The values are lengths of palindrome at index `i`.

One of the auxiliary arrays saves previous states. Another saves ongoing states. Starting from the last index, compare characters one by one. If two characters are the same, update the current length using the previous state.
Decrement the starting index and repeat.

#### Solution
- Python

```python
class LongestPalindromicSubsequence:
    def longestPalindromeSubseq(self, s: str) -> int:
        n = len(s)
        if s == s[::-1]: return n
        prev = [0 for _ in range(n)]
        for i in range(n-1, -1, -1):
            cur = [0 for _ in range(n)]
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
- Time: `O(n^2)` -- n is a length of the given string
- Space: `O(n)`
