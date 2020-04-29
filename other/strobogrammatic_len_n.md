# Strobogrammatic Number 2 -- Length N

#### Description

Given an integer `n`,  find all strobogrammatic numbers of length `n`.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

#### Example 1

Input: `n = 2`

Output: `["11","69","88","96"]`

#### Example 2

Input: `n = 1`

Output: `["0","1","8"]`

#### How to Solve

Among a couple of approaches, the recursion would be easier to solve this problem. The solution here makes string from left and right edges. Those two strings are expanding to inside one by one. The characters to add left and right sides are a rotated pair. The string length decreases by 2 since two characters are added in the single iteration. In the end, the length becomes 0 or 1 (n is even or odd). This is the terminal condition.

- Similar problems
    - [Confusing Number](confusing_number.md)
    - [Confusing Number 2 -- Up to N](confusing_number_upto_n.md)
    - [Strobogrammatic Number](strobogrammatic.md)

#### Solution
- Python

```python
class StrobogrammaticLenN:
    def findStrobogrammatic(self, n: int) -> 'List[str]':
        def walk(l, left, right):
            if l == 0:
                result.append(left+right)
                return
            if l == 1:
                for d in '018':
                    result.append(left+d+right)
                return
            if l == n:
                for d in '1689':
                    walk(l-2, left+d, mapping[d]+right)
            else:
                for d in '01689':
                    walk(l-2, left+d, mapping[d]+right)

        mapping = {'0': '0', '1': '1', '6': '9', '8': '8', '9': '6'}
        result = []
        walk(n, '', '')
        return result
```

#### Complexity
- Time: `O(5^n)` -- n is a given integer
- Space: `O(n)`
