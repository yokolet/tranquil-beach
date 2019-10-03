# Backspace String Compare

#### Description

Given two strings `S` and `T` includes `#` as a backspace, return true if they are equal after all characters are typed. It not, return false.

#### Example 1
Input: `S = "ab#c", T = "ad#c"`

Output: `True`

Explanation: Both become `"ac"`

#### Example 2
Input: `S = "ab##", T = "c#d#"`

Output: `True`

Explanation: Both become `""`

#### Example 3
Input: `S = "a##c", T = "#a#c"`

Output: `True`

Explanation: Both become `"c"`

#### Example 4
Input: `S = "a#c", T = "b"`

Output: `False`

Explanation: They become `"c"` and `"b"`

#### How to Solve

Use stack to find characters after all are typed. If the character is not `#`, append the stack. If the character is `#` and the stack is not empty, pop from the stack. In the end, compare two stacks.

#### Solution
- Python

```python
class Backspace:
    def backspaceCompare(self, S: str, T: str) -> bool:
        def edited(w):
            stack = []
            for c in w:
                if c != '#':
                    stack.append(c)
                elif stack:
                    stack.pop()
            return stack
        
        return edited(S) == edited(T)
```

#### Complexity
- Time: `O(n+m)` -- n, m are the lengths of S and T
- Space: `O(n+m)`
