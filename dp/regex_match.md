# Regular Expression Matching

#### Description

Given an input string (s) and a pattern (p), implement regular expression matching with support for `"."` and `"*"`.
The matching should cover the entire input string (not partial).

- `"."` Matches any single character.
- `"*"` Matches zero or more of the preceding element.

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like `"."` or `"*"`.

#### Example 1
Input: `s = "aa"`, `p = "a"`

Output: False

Explanation: `p = "a"` matches only one `"a"`.

#### Example 2
Input: `s = "aa"`,  `p = "a*"`

Output: True

Explanation: `p = "a*"` matches any number of `"a"`s.

#### Example 3
Input: `s = "ab"`, `p = ".*"`

Output: True

Explanation: `p = ".*"` matches any number of any characters.

#### Example 4
Input: `s = "aab"`, `p = "c*a*b"`

Output: True

Explanation: `p = "c*a*b"` matches any number (including zero) of `"c"`s, followed by any number of `"a"`s, then followed by one `"b"`.

#### Example 5
Input: `s = "mississippi"`, `p = "mis*is*p*."`

Output: False

Explanation: `p = "mis*is*p*."` doesn't match the third `"i"`, so the pattern is for `"mississppi"`. 

#### How to Solve

The solution here is a dynamic programming approach by recursion.
It saves the previous state in a dictionary whose key is indices of s and p, `(i, j)`. The value is the result of matching at `(i, j)` - boolean.
Only when the j-th pattern is `"*"`, the index `j` shifts more than 1, while the index `i` may shift one.  
Other cases increment two indices by one.

Recursively checking the characters and the previous state,
the result is found at the key `(0, 0)`.

#### Solution
- Python

```python
class RegexMatch:
    def isMatch(self, s: str, p: str) -> bool:
        memo = {}
        def isMatchRecur(i: int, j:int) -> bool:
            if (i, j) not in memo:
                if j == len(p):
                    result = i == len(s)
                else:
                    result = i < len(s) and p[j] in ['.', s[i]]
                    if j + 1 < len(p) and p[j + 1] == '*':
                        result = isMatchRecur(i, j + 2) or (result and isMatchRecur(i + 1, j))
                    else:
                        result = result and isMatchRecur(i + 1, j + 1)
                memo[i, j] = result
            return memo[i, j]
        return isMatchRecur(0, 0)
```

- Ruby

```ruby
# @param {String} s
# @param {String} p
# @return {Boolean}
def is_match(s, p)
  is_match_recur(s, p, 0, 0, {})
end

def is_match_recur(s, p, i, j, memo)
  unless memo.has_key?([i, j])
    if j == p.size
      memo[[i, j]] = i == s.size
    else
      memo[[i, j]] = i < s.size && ['.', s[i]].include?(p[j])
      if j + 1 < p.size && p[j + 1] == '*'
        memo[[i, j]] = is_match_recur(s, p, i, j + 2, memo) || (memo[[i, j]] && is_match_recur(s, p, i + 1, j, memo))
      else
        memo[[i, j]] = memo[[i, j]] && is_match_recur(s, p, i + 1, j + 1, memo)
      end
    end
  end
end
```

#### Complexity
- Time: O(2^m) -- m is a length of pattern 
- Space: O(n*m) -- n is a length of string