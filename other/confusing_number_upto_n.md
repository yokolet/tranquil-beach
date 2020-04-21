# Confusing Number 2 -- Up to N

#### Description

Given a positive integer `N`, return the number of confusing numbers between 1 and `N` inclusive. The definition of confusing number is below:

- Definition
    - Digits can be rotated by 180 degrees if those are 0, 1, 6, 8, 9.
    - Any digits of 2, 3, 4, and 5 are invalid.
    - The confusing number is a number that becomes a different number when it is rotated 180 degrees.

#### Example 1

Input: `20`

Output: `6`

Explanation: confusing numbers are: `6,9,10,16,18,19`

#### Example 2

Input: `100`

Output: `19`

Explanation: confusing numbers are: `6,9,10,16,18,19,60,61,66,68,80,81,86,89,90,91,98,99,100`

#### How to Solve

The basic idea is not so difficult. Create possible combinations of confusing number under given `N`, check if those are not symmetric if rotated. However, this problem easily gets a time limie exceeded error.
How to make it run faster is the key.

The solution here took depth first search (DFS) approach.
Starting from 1,6,8,9, go deeper while adding digits, 0,1,6,8,9 one by one. If the created number is less than the given value and is not symmetric (rotated number is the same as original), count up.

- Similar problems
    - [Strobogrammatic Number](strobogrammatic.md)
    - [Confusing Number](confusing_number.md)

#### Solution
- Python

```python
class ConfusingNumberUptoN:
    def confusingNumberII(self, N: int) -> int:
        def symmetric(n):
            s = str(n)
            l, r = 0, len(s)-1
            while l <= r:
                if s[l] != mapping[s[r]]: return False
                l += 1
                r -= 1
            return True
        
        def dfs(n, count):
            if int(n) > N: return count
            if not symmetric(n):
                count += 1
            for c in '01689':
                count = dfs(n+c, count)
            return count

        mapping = {'0':'0', '1':'1', '6':'9', '8':'8', '9':'6'}
        count = 0
        for i in '1689':
            count = dfs(i, count)
        return count
```

#### Complexity
- Time: `O(5^n)` -- n is a number of digits in the given integer
- Space: `O(n)`
