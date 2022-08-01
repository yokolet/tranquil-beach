# Single Number

#### Description
Given a non-empty array of integers `nums`, every element appears **twice** except for one.
Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

#### Examples
##### Example 1
Input: nums = `[2,2,1]`

Output: `1`

Explanation: `1` is a single number

##### Example 2
Input: nums = `[4,1,2,1,2]`

Output: `4`

Explanation: `4` is a single number

##### Example 3
Input: nums = `[1]`

Output: `1`

Explanation: `1` is a single number

#### How to Solve

There are a couple of ways to solve this problem. For example, using an auxiliary dictionary or
array, or mathematical calculation. Among those, a solution by bit manipulation is a good one.
It doesn't use extra space, and going over the given array just once will give us the answer.
In this case, `XOR` is the operator.
The `XOR` gives 0 if the both side of the operator are the same number.
Only repeating the `XOR` is enough for this solution.

#### Solution
- Python

```python
class SingleNumber:
    def singleNumber(self, nums: List[int]) -> int:
        result = nums[0]
        for i in range(1, len(nums)):
            result ^= nums[i]
        return result
```

#### Complexity
- Time: `O(n)` -- n is a length of nums
- Space: `O(1)`
