# Wildcard Matching

#### Description

Given an input string `s` and a pattern `p`, implement wildcard pattern matching with support for `"?"` and `"*"`.

- `"?"` Matches any single character.
- `"*"` Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial). The input string `s` could be empty and contains only lowercase letters a-z.
The pattern `p` could be empty and contains only lowercase letters a-z, `"?"` or `"*"`.


#### Example 1
Input: `s = "aa"`, `p = "a"`

Output: False

Explanation: pattern`"a"` only matches a single char `"a"`

#### Example 2
Input: `s = "aa"`, `p = "*"`

Output: True

Explanation: `"*"` matches any length of any characters

#### Example 3
Input: `s = "cb"`, `p = "?a"`

Output: False

Explanation: `"?a"`matches any single character followed by a single char `"a"`

#### Example 4
Input: `s = "adceb"`, `p = "*a*b"`

Output: True

Explanation: `"*"` matches any length including zero, so `"a*b"` matches `"a"`, `"dce"`, and `"b"`

#### Example 5
Input: `s = "acdcb"`, `p = "a*c?b"`

Output: False

Explanation: `"a*c?"` matches `"acd"`, but next `"c"` doesn't match.

#### How to Solve

Use four pointers. Two are normal pointers for a string `s` and pattern `p`.
When `"*"` comes, it matches any length including zero, so save the indices as extra pointers. Increment those pointers checking each characters.

#### Solution
- Python

```python
class Wildcard:
    def isMatch(self, s: str, p: str) -> bool:
        i, j, star_i, star_j = 0, 0, None, None
        while i < len(s):
            if j < len(p) and p[j] == '*':
                star_i, star_j = i, j
                j += 1
            elif j < len(p) and (s[i] == p[j] or p[j] == '?'):
                i += 1
                j += 1
            elif star_i is not None:
                i, j = star_i + 1, star_j + 1
                star_i += 1
            else:
                return False
        while j < len(p) and p[j] == '*':
            j += 1
        return j == len(p)
```

- Ruby

```ruby
# @param {String} s
# @param {String} p
# @return {Boolean}
def is_match(s, p)
  i, j, star_i, star_j = 0, 0, -1, -1
  while i < s.size
    if j < p.size && p[j] == '*'
      star_i, star_j = i, j
      j += 1
    elsif j < p.size && (s[i] == p[j] || p[j] == '?')
      i += 1
      j += 1
    elsif star_i >=0
      i, j = star_i + 1, star_j + 1
      star_i += 1
    else
      return false
    end
  end
  while j < p.size && p[j] == '*'
    j += 1
  end
  j == p.size
end
```

#### Complexity
- Time: `O(m+n)` -- m,n are the lengths of s, p
- Space: `O(1)`
