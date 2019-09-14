# Longest Substring Without Repeating Characters

#### Description

Given a string, find the length of the longest substring without repeating characters.

#### Example 1
Input: `"abcabcbb"`

Output: `3`

Explanation: "abc" is the longest substring.

#### Example 2
Input: `"bbbbb"`

Output: `1`

Explanation: "b" is the longest substring.

#### Example 3
Input: `"pwwkew"`

Output: `3`

Explanation: "wke" is the longest substring.

#### How to Solve

The solution saves the last occurence of each character in a Dictionary (Hash for Ruby). When a current character is found in a dictionary, it updates the last non-duplicate index. The max length is updated comparing the last non-dupliate length at index i.

#### Solution
- Python

```python
class LongestSubstring:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left, max_len, memo = 0, 0, {} # char to index map
        for i in range(len(s)):
            if s[i] in memo:
                left = max(left, memo[s[i]])    
            max_len = max(max_len, i - left + 1)
            memo[s[i]] = i + 1
        return max_len
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def length_of_longest_substring(s)
  left, max_length, memo = 0, 0, {}
  s.size.times do |i|
    if memo.has_key?(s[i])
      left = [left, memo[s[i]]].max
    end
    max_length = [max_length, i - left + 1].max
    memo[s[i]] = i + 1
  end
  max_length
end
```

#### Complexity
- Time: O(n)
- Space: O(1) -- auxiliary map will have some fixed number of keys, a-z, A-Z, 0-9, space or such.