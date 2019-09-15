# Reverse Substrings Between Each Pair of Parentheses

#### Description

Given a string `s` which consists of lower case English letters and parentheses, reverse the strings in each pair of matching parentheses. The reversal should start from the innermost matching pair.

#### Example 1

Input: `s = "(abcd)"`

Output: `"dcba"`

#### Example 2

Input: `s = "(u(love)i)"`

Output: `"iloveu"`

#### Example 3

Input: `s = "(ed(et(oc))el)"`

Output: `"leetcode"`

#### Example 4

Input: `s = "a(bcdefghijkl(mno)p)q"`

Output: `"apmnolkjihgfedcbq"`

#### How to Solve

A recursion is an approach used to solve the problem.
Add a character one by one until `(` is found.
When it comes to `(`, go deeper stack and repeat adding character as a new substring.
When it comes to `)`, reverse the substring between `(` and `)`, then return it.
When it returns from deeper stack, add the substring as a prefix, then repeat adding characters as suffix.  

#### Solution

- Python

```python
class ReverseStrInParen:
    def reverseParentheses(self, s: str) -> str:
        n = len(s)

        def walk(idx):
            result = ''
            while idx < n:
                if idx < n and s[idx] == '(':
                    idx += 1
                    idx, tmp = walk(idx)
                    result += tmp
                if idx < n and s[idx] == ')':
                    idx += 1
                    return (idx, result[::-1])
                if idx < n and s[idx] not in ['(', ')']:
                    result += s[idx]
                    idx += 1
            return (idx, result)

        _ ,  result = walk(0)
        return result
```

#### Complexity

- Time: `O(n)` -- n is a length of given string 
- Space: `O(d)` -- d is a depth of parentheses
