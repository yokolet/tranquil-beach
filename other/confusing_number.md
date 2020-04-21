# Confusing Number

#### Description

Given a number `N`, return `True` if and only if it is a confusing number. The definition of confusing number is below:

- Definition
    - Digits can be rotated by 180 degrees if those are 0, 1, 6, 8, 9.
    - Any digits of 2, 3, 4, and 5 are invalid.
    - The confusing number is a number that becomes a different number when it is rotated 180 degrees.

#### Example 1

Input: `6`

Output: `True`

Explanation: `6` becomes `9`.

#### Example 2

Input: `89`

Output: `True`

Explanation: `89` becomes `68`.

#### Example 3

Input: `11`

Output: `False`

Explanation: `11` becomes `11`, which is the same number.

#### Example 4

Input: `25`

Output: `False`

Explanation: Both `2` and `5` are invalid.

#### How to Solve

Use a mapping table to convert a digit to rotated one. After converted the given number to string, create the rotated number adding next digit on the top. If invalid number is found, return `False`. Otherwise, check the number in the end whether it is the same as original or not.

- Similar problems
    - [Strobogrammatic Number](strobogrammatic.md)
    - [Confusing Number 2 -- Up to N](confusing_number_upto_n.md)

#### Solution
- Python

```python
class ConfusingNumber:
    def confusingNumber(self, N: int) -> bool:
        mapping = {'0':'0', '1':'1', '8':'8', '9':'6', '6':'9'}
        orig, rot = str(N), ''
        for c in orig:
            if c not in mapping: return False
            rot = mapping[c] + rot
        return orig != rot
```

#### Complexity
- Time: `O(n)` -- n is a number of digits in the given integer
- Space: `O(1)`
