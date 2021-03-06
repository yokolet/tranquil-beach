# Valid Palindrome

#### Description

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Assume an empty string is valid palindrome.

#### Example 1
Input: `"A man, a plan, a canal: Panama"`

Output: true

#### Example 2
Input: `"race a car"`

Output: false

#### How to Solve

Make all characters to lower case then delete characters which are not a to z or 0 to 9. Lastly, check the string is a palindrome.

Python has a nice built-in function -- `str.translate` and `str.maketrans`, which runs faster than regular expression.
The second Python solution uses this function.
The first line in the solution, `str.maketrans('', '', string.punctuation + ' ')`, defines no substitution but deletetion of punctuations and spaces. When the rule is fed to `str.translate`, the string has only a-z and 0-9.

Ruby solution uses regular expression which runs fast.
Like Python code, it makes all characters to lower case then deletes characters other than a to z or 0 to 9.

#### Solution
- Python

```python
import re

class ValidPalindrome:
    def isPalindrome(self, s: 'str') -> 'bool':
        s = re.sub(r'[^a-z0-9]', '', s.lower())
        return s == s[::-1]
```

```python
import string

class ValidPalindrome:
    def isPalindrome(self, s: str) -> bool:
        translator = str.maketrans('', '', string.punctuation + ' ')
        s = s.lower().translate(translator)
        return s == s[::-1]
```

- Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_palindrome(s)
  return true if s.size == 1
  s = s.downcase.delete '^a-z0-9'
  s == s.reverse
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(1)`
