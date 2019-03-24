# Palindromic Substrings

#### Description

Given a string, find how many palindromic substrings are in the string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

#### Example 1
Input: `"abc"`

Output: `3`

Explanation: palindromes are: "a", "b", "c".

#### Example 2
Input: `"aaa"`

Output: `6`

Explanation: palindromes are: "a", "a", "a", "aa", "aa", "aaa".

#### How to Solve

This solution uses two pointers for the starting index as left and expanding index as right. Outer while loop proceeds left index, while inner two while loop checks the character and counts palindromes. The first inner while loop is to check whether the same character continues or not. After the first inner loop, the code counts how many of palindromes by the same character were found.

For example, substring is `"aaa"`, the palindromes are: `"a", "a", "a", "aa", "aa", "aaa"`. 

|length of palindrome  | 1 | 2 | 3 |
|---------------------:|--:|--:|--:|
|number of palindromes | 3 | 2 | 1 |

In total, `3+2+1 = 6` which can be calculated by `n*(n+1)/2`.

The second inner loop expands the range to both sides one by one. While it is the palindrome, the count increases 1 each.

When the two inner loop finishes, the next starting index (left) is the current right index.


#### Solution
- Python

```python
class CountPalindromes:
    def countSubstrings(self, s: 'str') -> 'int':
        if not s: return 0
        result, left = 0, 0
        while left < len(s):
            right = left + 1
            # the same character may continue
            while right < len(s) and s[left] == s[right]:
                right += 1
            result += (right-left) * (right-left+1) // 2
            l = left - 1
            r = right
            # expand while it is palindrome
            while l >= 0 and r < len(s) and s[l] == s[r]:
                l -= 1
                r += 1
                result += 1
            left = right
        return result
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def count_substrings(s)
  return 0 if s.nil? || s.empty?
  result, left = 0, 0
  while left < s.size
    right = left + 1
    while right < s.size && s[right] == s[left]
      right += 1
    end
    result += (right - left) * (right - left + 1) / 2
    l = left - 1
    r = right
    while l >= 0 && r < s.size && s[l] == s[r]
      l -= 1
      r += 1
      result += 1
    end
    left = right
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(1)