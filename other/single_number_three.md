# Single Number -- Three

#### Description
Given an integer array `nums`, in which exactly two elements appear only once and all the other elements appear exactly twice.
Find the two elements that appear only once. You can return the answer in any order.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.


#### Examples
##### Example 1
Input: nums = `[1,2,1,3,2,5]`

Output: `[3,5]`

Explanation: 3 and 5 appear only once, others are twice

##### Example 2
Input: nums = `[-1,0]`

Output: `[-1, 0]`

Explanation: -1 and 0 appear only once

#### How to Solve

Like Single Number nad Single Number Two problems, a bit manipulation is a good way to solve this problem.
In this case, if all numbers are `XOR`-ed, `x ^ y` will be left.
Next step is how to figure out these two numbers.
For this purpose, `a & (~(a - 1))` is used.
Then, `AND` operator is used for all numbers in the given array.
If `AND` result is not 0, the number is `XOR`-ed with one of two single numbers.
If not, the number is also `XOR`-ed with another of two single numbers.
When the loop is over, we get two single numbers.

#### Solution
- Python

```python
class SingleNumberThree:
    def singleNumber(self, nums: List[int]) -> List[int]:
        a = 0
        for n in nums:
            a ^= n
        diff = a & (~(a - 1))
        a, b = 0, 0
        for n in nums:
            if n & diff:
                a ^= n
            else:
                b ^= n
        return [a, b]
```

#### Complexity
- Time: `O(n)` -- n is a length of nums
- Space: `O(1)`
