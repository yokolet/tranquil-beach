# Maximum Size Subarray Sum Equals k

#### Description

Given an array of integers and a target value k, find the maximum length of a subarray that sums to k. Return 0 if such subarray doesn't exist.

#### Example 1
Input: `nums = [1, -1, 5, -2, 3]`, `k = 3`

Output: 4 

Explanation: `[1, -1, 5, -2]` sums to 3 and is the longest.

#### Eaxample 2
nput: `nums = [-2, -1, 2, 1]`, `k = 1`

Output: 2 

Explanation: `[-1, 2]` sums to 1 and is the longest.

#### How to Solove

Use dictionary (Hash in Ruby) to save the state so far.
The dictionary's key is a total sum from 0 to index i, and the value is its index. If duplicates are there, it doesn't update since the problem asks the longest subarray.
If accumulated sum - k exists in the dictionary, the current index value sums up to k. So, check the length.

Tricky part of this problem is accumulated sum is 0. When the sum is zero, all index up to the current index should be included. For this reason, the dicionary should have `{0: -1}` in any case.

This way, the longest subarray will be found.

#### Solution
- Python

```python
class MaxSubarraySumK:
    def maxSubArrayLen(self, nums: 'List[int]', k: int) -> int:
        max_len, acc, memo = 0, 0, {0: -1} # {sum: index}
        for i in range(len(nums)):
            acc += nums[i]
            if acc - k in memo:
                max_len = max(max_len, i - memo[acc - k])
            if acc not in memo:
                memo[acc] = i
        return max_len
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def max_sub_array_len(nums, k)
  max_length, sum_sofar, memo = 0, 0, {0 => -1}
  nums.each_with_index do |v, i|
    sum_sofar += v
    if memo.has_key?(sum_sofar - k)
      max_length = [max_length, i - memo[sum_sofar - k]].max
    end
    unless memo.has_key?(sum_sofar)
      memo[sum_sofar] = i
    end
  end
  max_length
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(n)`