# Valid Palindrome by Deleting a Character

#### Description

Given a non-empty string s, judge whether s can be a palindrome by deleting at most one character.

The string contains lowercase characters a-z. The maximum length of the string is 50000.

#### Example 1
Input: `"aba"`

Output: `true`

#### Example 2
Input: `"abca"`

Output: `true`

Explanation: Deleting the character 'c' makes the string palindrome.

#### How to Solve

The length 1 string is obviously a palindrome.
The length 2 string will be a palindrome by deleting one character.
When the string itself isn't a palindrome, start checking characters one by one.

The solution is checking two chars from the first and last.
If the two chars is not the same, check left + 1 to right is a palindrome. If failed, check left to right - 1 is a palindrome.

#### Solution
- Python

```python
class PalindromeByDeletion:
    def validPalindrome(self, s: 'str') -> 'bool':
        n = len(s)
        if n <= 2 or s == s[::-1]: return True
        left, right = 0, n - 1
        while left < right and s[left] == s[right]:
            left += 1
            right -= 1
        return s[left+1:right+1] == s[left+1:right+1][::-1] or\
                s[left:right] == s[left:right][::-1]
```

- Ruby

```ruby
# @param {String} s
# @return {Boolean}
def valid_palindrome(s)
  n = s.size
  return true if n <= 2 || s == s.reverse
  left, right = 0, n - 1
  while left < right
    if s[left] == s[right]
      left += 1
      right -= 1
    else
      return s[left+1..right] == s[left+1..right].reverse ||
              s[left...right] == s[left...right].reverse
    end
  end
  true
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(1)`
