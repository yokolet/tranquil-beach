# Continuous Subarray Sum n*k

#### Description

Given an array of non-negative integers and a target integer k, find if the array has a continuous subarray of size at least 2 that sums up to the multiple of k.

The length of the array won't exceed 10,000.
The sum of all the numbers is in the range of a signed 32-bit integer.

#### Example 1
Input: `nums = [23, 2, 4, 6, 7], k = 6`

Output: `True`

Explanation: [2, 4] is a continuous subarray of size 2 and sums up to 6.

#### Example 2
Input: `nums = [23, 2, 6, 4, 7], k = 6`

Output: `True`

Explanation: [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.

#### Example 3
Input: `nums = [0, 1, 0], k = 0`

Output: `False`

Explanation: there's no subarray of size 2 sum up to 0

#### How to Solve

Every number is expressed by `n * k + remainder`. Look at the example 1, `[23, 2, 4, 6, 7]`. The cummulative array of example 1 is `[23, 25, 29, 35, 42]`, which is expressed by `[3*6+5, 4*6+1, 4*6+5, 5*6+5, 7*6+0]`. The first and third cummulated values have the same remainder, which means `4*6+5 - 3*6+5 = (4-3)*6` -- divisible by k. The subarray from the second to third sums up to n*k.

Since only remainder contributes, save a pair of (cummulated sum % k) and index i in a dictionary. When the dictionary has the same remainder, check the length. 

#### Solution
- Python

```python
class SubarraySumNK:
    def checkSubarraySum(self, nums: 'List[int]', k: int) -> bool:
        sum, memo = 0, {0: -1}
        for i in range(len(nums)):
            if k != 0:
                sum = (sum + nums[i]) % k
            else:
                sum += nums[i]
            if sum in memo:
                if i - memo[sum] >= 2: return True
            else:
                memo[sum] = i
        return False
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Boolean}
def check_subarray_sum(nums, k)
  sum, memo = 0, {0 => -1}
  nums.size.times do |i|
    if k != 0
      sum = (sum + nums[i]) % k
    else
      sum += nums[i]
    end
    if memo.has_key?(sum)
      return true if i - memo[sum] >= 2
    else
      memo[sum] = i
    end
  end
  false
end
```

#### Complexity
- Time: O(n)
- Space: O(k)