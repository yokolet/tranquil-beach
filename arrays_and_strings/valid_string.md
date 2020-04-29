# Valid Parenthesis String

#### Description

Given a string containing only `'('`, `')'` and `'*'`, determine the string is valid. The validity of the string is defined below:

- Definition
    - Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
    - Any right parenthesis `')'` must have a corresponding left prenthesis `'('`.
    - The left parenthesis must appear before the corresponding right parenthesis.
    - `'*'` could be a single left/right parenthesis or an empty string.
    - An empty string is valid

#### Example 1

Input: `()`

Output: True

#### Example 2

Inpput: `(***)`

Output: True

#### Example 3

Inpput: `(*))`

Output: True

#### How to Solve

A bruto force solution gets a Time Limit Exceeded error. How to make it run faster is a key to solve this problem.

The solution here counts left parenthesis at each index of the input string. Since the `'*'` (star) can be a left parenthesis, maximum left parenthesis count is maintained at each index.

The maximum counts should be positive. When it goes to negative, stop counting. The minimum counts should be greater than zero. So, the value is adusted when it turns to negative.

In the end, if the minimum count is zero, the string is valid.

#### Solution
- Python

```python
class ValidString:
    def checkValidString(self, s: str) -> bool:
        left_min, left_max = 0, 0
        for c in s:
            if c == '(': left_min += 1
            else: left_min -= 1
            if c in ['(', '*']: left_max += 1
            else: left_max -= 1
            if left_max < 0: break
            left_min = max(left_min, 0)
        return left_min == 0
```

#### Complexity
- Time: `O(n)` -- n is a legnth of the input string
- Space: `O(1)`
