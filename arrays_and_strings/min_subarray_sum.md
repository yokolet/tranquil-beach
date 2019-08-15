# Minimum Size Subarray Sum

#### Description

Given an array of positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

#### Example
Input: `s = 7`, `nums = [2,3,1,2,4,3]`

Output: `2`

Explanation: `[4,3]` is the minimal length

#### How to Solve

Two pointers are used here.
The left pointer goes forward only when the sum is greater than or equal to s. The right pointer goes forward one by one.
The accumulated sum will be decreased when left pointer goes forward and increated when right pointer goes forward.

#### Solution
- Python

```python
class MinSubarraySum:
    def minSubArrayLen(self, s: int, nums: 'List[int]') -> int:
        n = len(nums)
        if n == 0 or (n == 1 and nums[0] < s): return 0
        acc, left, min_len = 0, 0, n + 1
        for i in range(n):
            acc += nums[i]
            while acc >= s:
                min_len = min(min_len, i - left + 1)
                acc -= nums[left]
                left += 1
        return min_len if min_len <= n else 0
```

- Ruby

```ruby
# @param {Integer} s
# @param {Integer[]} nums
# @return {Integer}
def min_sub_array_len(s, nums)
  n = nums.size
  return 0 if nums == 0 || (n == 1 && nums[0] < s)
  acc, left, min_len = 0, 0, n + 1
  (0...n).each do |i|
    acc += nums[i]
    while acc >= s
      min_len = [min_len, i - left + 1].min
      acc -= nums[left]
      left += 1
    end
  end
  min_len <= n ? min_len : 0
end
```

#### Complexity
- Time: `O(n)` -- since two pointers go through once
- Space: `O(1)`