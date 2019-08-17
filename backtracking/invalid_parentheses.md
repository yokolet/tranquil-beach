# Remove Invalid Parentheses

#### Description

Given a string containing letters and invalid parentheses,`(` and `)`, remove the minimum number of invalid parentheses to make the string valid. Return all possible results.

#### Example 1
Input: `"()())()"`

Output: `["()()()", "(())()"]`

#### Exmaple 2
Input: `"(a)())()"`

Output: `["(a)()()", "(a())()"]`

#### Example 3
Input: `")("`

Output: `[""]`

#### How to Solve

The solution takes a recursive approach. A given string is processed from left to right, then right to left. While going over the string, two pointers are used. The right index is incremented until closing parens are less than or equal to opening parens. When parens become invalid (closing parens exceed opening parens by the counts), the closing paren at the left index is removed. This shorter string is hand over to the same process with left and right indices at that point. Recursively, it repeats by incrementing the left pointer. The string may be balanced if the opening paren is removed. When the right pointer reaches to the end of the string, a reversed string is checked with the reversed opening and closing parens. When the reversed string comes back, it is a reversed balanced string. So, the reversed string is added to the result.

#### Solution
- Python

```python
class InvalidParentheses:
    def removeInvalidParentheses(self, s: str) -> 'List[str]':
        def remove(s, left, right, parens):
            count = 0
            while right < len(s):
                if s[right] == parens[0]:
                    count += 1
                elif s[right] == parens[1]:
                    count -= 1
                
                if count >= 0:
                    right += 1
                    continue
                
                start = left
                while left <= right:
                    if s[left] == parens[1] and (left == start or s[left - 1] != parens[1]):
                        remove(s[:left] + s[left+1:], left, right, parens)
                    left += 1
                return

            if parens[1] == ')':
                remove(s[::-1], 0, 0, (')', '('))
            else:
                result.append(s[::-1])

        result = []
        remove(s, 0, 0, ('(', ')'))
        return result
```

- Ruby

```ruby
# @param {String} s
# @return {String[]}
def remove_invalid_parentheses(s)
  result, parens = [], ['(', ')']
  remove(s, 0, 0, parens, result)
  result
end
def remove(s, last_i, last_j, parens, result)
  i, count  = last_i, 0
  while i < s.size
    count += 1 if s[i] == parens[0]
    count -= 1 if s[i] == parens[1]
    if count >= 0
      i += 1
      next
    end
    j = last_j
    while j <= i
      if s[j] == parens[1] && (j == last_j || s[j-1] != s[j])
        remove(s[0...j]+s[j+1..-1], i, j, parens, result)
      end
      j += 1
    end
    return
  end
  if parens[1] == ')'
    remove(s.reverse, 0, 0, [')', '('], result)
  else
    result << s.reverse
  end
end
```

##### Complexity
- Time: `O(2^n)`
- Space: `O(n)`