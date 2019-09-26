# Happy Number

#### Description

Given an integer `n`, write an algorithm to determine `n` is happy. Return True if `n` is happy. If not or loops endlessly, return False.

- Definition

    The integer `n` is happy when a repetition of a square sum of each digit becomes 1 (the square sum of the square sum of ...). If it becomes other than 1 or oscilates, the given integer is not happy.

#### Example
Input: `19`

Output: `True`

Explanation:

```
1 * 1 + 9 * 9 = 82
8 * 8 + 2 * 2 = 68
6 * 6 + 8 * 8 = 100
1 * 1 + 0 * 0 + 0 * 0 = 1
```

#### How to Solve

Use set to detect a cycle. If the square sum is in the set, return False. Otherwise, continue calculating the square sum unless sum is equal to 1.

#### Solution

- Python

```python
class HappyNumber:
    def isHappy(self, n: int) -> bool:
        if not n: return False

        def squareSum(v):
            sum, carry = 0, v
            while carry:
                carry, rem = divmod(carry, 10)
                sum += rem*rem
            return sum

        sum = squareSum(n)
        seen = {n}
        while sum != 1:
            sum = squareSum(sum)
            if sum in seen: return False
            seen.add(sum)
        return True
```

#### Complexity
- Time: `O(mn)` - m, n are a number of square sum repetition and digits
- Space: `O(m)`
