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
If sum_sofar - k exists in the dictionary, the current index value sums up to k. So, check the length. This way, the longest subarray will be found.

#### Solution
- Python

```python
class MaxSubarraySumK:
    def maxSubArrayLen(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        max_length, sum_sofar, memo = 0, 0, {0: -1} # {sum: index}
        for i in range(len(nums)):
            sum_sofar += nums[i]
            if sum_sofar - k in memo:
                max_length = max(max_length, i - memo[sum_sofar - k])
            if sum_sofar not in memo:
                memo[sum_sofar] = i
        return max_length
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
- Time: O(n)
- Space: O(n)