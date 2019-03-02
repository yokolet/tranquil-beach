# Valid Parentheses

#### Description

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- open brackets must be closed by the same type of brackets.
- open brackets must be closed in the correct order.
- an empty string.

#### Example 1
Input: `s = "()[]{}"`

Output: `True`

#### Example 2
Input: `s = "([)]"`

Output: `False`

#### Example 3
Input: `s = "{[]}"`

Output: `True`

#### How to Solve

Use stack to save opening parens.
If closing paren is found, check the top of stack is the matching opening paren or not. If yes, pop the opening paren from the stack. If no, the string is not valid.

In the end, check stack is empty. If yes, the string is a valid parenthese. If not, some opening parens are left without matching closing paren. So, return false.


#### Solution
- Python

```python
class ValidParentheses:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        pairs = {
            ')': '(',
            '}': '{',
            ']': '['
        }
        for c in s:
            if c in pairs:
                # closing paren
                if len(stack) > 0 and stack[-1] == pairs[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return len(stack) == 0
```

- Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_valid(s)
  return true if s.empty?
  stack = []
  pairs = {
      ')' => '(',
      ']' => '[',
      '}' => '{'
  }
  s.size.times do |i|
    c = s[i]
    if pairs.has_key?(c) # closing paren
      if stack.size > 0 && (stack[-1] == pairs[c])
        stack.pop
      else
        return false
      end
    else
      stack.push(c)
    end
  end
  stack.empty?
end
```

#### Complexity
- Time: O(n)
- Space: O(n)