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

The solution takes two steps of recursive approach. The first step is from the start to end of the given string. The second step is from the end to start. It counts starting and ending parentheses. When closing paren for the first step exceeds opening, the closing paren will be removed. The shorter string is checked recursively. The string may be balanced when the opening paren is removed. This is done in the second step.

#### Solution
- Python

```python
class InvalidParentheses:
    def removeInvalidParentheses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        def remove(s, last_i, last_j, parens, result):
            i, count = last_i, 0
            while i < len(s):
                if s[i] == parens[0]:
                    count += 1
                elif s[i] == parens[1]:
                    count -= 1
                
                if count >= 0:
                    i += 1
                    continue
                
                j = last_j
                while j <= i:
                    if s[j] == parens[1] and (j == last_j or s[j - 1] != s[j]):
                        remove(s[:j] + s[j+1:], i, j, parens, result)
                    j += 1
                return

            if parens[1] == ')':
                remove(s[::-1], 0, 0, (')', '('), result)
            else:
                result.append(s[::-1])

        result = []
        remove(s, 0, 0, ('(', ')'), result)
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
- Time: O(2^n)
- Space: O(n)