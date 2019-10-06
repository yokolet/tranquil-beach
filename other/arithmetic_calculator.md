# Basic Calculator -- Arithmetic Calculator

#### Description

Implement a basic calculator to evaluate a string which conatins arithmetic operations. The given string contains only non-negative integers, `+`, `-`, `*`, `/` operators and spaces. The integer division should truncate toward zero.

#### Example 1
Input: `3+2*2`

Output: `7`

#### Example 2
Input: ` 3/2 `

Output: `1`

#### Example 3
Input: ` 3+5 / 2 `

Output: `5`

#### How to Solve

Basically, the given expression string is parsed from left to right. Addition and subtraction are easy. The key to solve this problem is how to handle a product and division. For this reason, the calculation is one step delayed. The last value before operation is handed over to the next operation. When the current character is a operator or the end of the string, the solution calculates the previous operation. In the end, the last value is still there, so add it up to the accumulated value.

#### Solution
- Python

```python
class ArithmeticCalculator:
    def calculate(self, s: str) -> int:
        last, v, acc, op = 0, 0, 0, '+'
        for i, c in enumerate(s):
            if c.isdigit():
                v = v*10 + int(c)
            if c in '+-*/' or i == len(s)-1:
                if op == '+':
                    acc += last
                    last = v
                elif op == '-':
                    acc += last
                    last = -v
                elif op == '*':
                    last *= v
                elif op =='/':
                    last = int(last / v)
                v = 0
                op = c
        return acc + last
```

#### Complexity
- Time: `O(n)` -- n is a length of the given string
- Space: `O(1)`
