# Single Number -- Two

#### Description
Given an integer array `nums` where every element appears **three times** except for one, which appears exactly once.
Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

#### Examples
##### Example 1
Input: nums = `[2,2,3,2]`

Output: 3

Explanation: 3 appears only once

##### Example 2
Input: nums = `[0,1,0,1,0,1,99]`

Output: 99

Explanation: 99 appears only once

#### How to Solve

Like the Single Number problem, a bit manipulation is a good choice to solve this problem.
It doesn't take extra space, and going over the given array just once gives us the answer.
However, this problem is not so easy since the same number appears three times.
It needs `AND` and `NOT` operators in addition to `XOR`.
```
a = 2        0 0 0 0 0 0 1 0
a ^ a        0 0 0 0 0 0 0 0
a ^ a ^ a    0 0 0 0 0 0 1 0
```
If `XOR` repeats three times, `a` will be left. Using `NOT` and `AND` operators:
```
~a           1 1 1 1 1 1 0 1
~a & a       0 0 0 0 0 0 0 0
```

#### Solution
- Python

```python
class SingleNumberTwo:
    def singleNumber(self, nums: List[int]) -> int:
        a, b = 0, 0
        for n in nums:
            a = ~b & (a ^ n)
            b = ~a & (b ^ n)
        return a
```

#### Complexity
- Time: `O(n)` -- n is a length of nums
- Space: `O(1)`
