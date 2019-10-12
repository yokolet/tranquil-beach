# Generate Parentheses

#### Description

Given n pairs of parentheses, generate all valid combinations of parentheses.

#### Example

Input: `3`

Output:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

#### How to Solve

Both BSF and DFS work to generate parentheses. When going to the next level, check how many opening and closing parenethess are left.

Unused closing parentheses should be always more than the unused opening parentheses. If the conditions meet, add a parenthesis and decrease the number of opening or closing parentheses. When none of opening and closeing parenthesis is left, add the generated string to the result list.

#### Solution

- Python

```python
class GenerateParentheses:
    def generateParenthesis(self, n: int) -> 'List[str]':
        result, queue = [], [('(', n-1, n)]
        while queue:
            p, left, right = queue.pop(0)
            if left == 0 and right == 0:
                result.append(p)
            if left > 0:
                queue.append((p+'(', left-1, right))
            if right > 0 and left < right:
                queue.append((p+')', left, right-1))
        return result
```

#### Complexity

- Time: `O(n)` -- n is a lengths of parentheses
- Space: `O(n)`
