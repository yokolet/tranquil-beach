# Maximum Sum of 3 Non-Overlapping Subarrays

#### Description

Given an array of positive integers, nums, and an integer, k, find three non-overlapping subarrays with maximum sum.

Each subarray size is k. Maximize the sum of all 3*k entries.

Return the result as a list of indices representing the starting position of each interval (0-indexed). If there are multiple answers, return the lexicographically smallest one.

#### Example
Input: `nums = [1,2,1,2,6,7,5,1], k = 2`

Output: `[0, 3, 5]`

Explanation: Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
The first subarray could be [2, 1], but an answer of [1, 3, 5] is considered as lexicographically larger.

#### How to Solve

The solution here takes a sliding window approach. Three windows start at indices, 0, k, 2*k. While sliding the windows one by one, check it is maximum sum or not. Since the problem asks the maximum of sum of three windows, the solution checks left sum, left max sum so far + mid sum, mid max sum so far + right sum.
When the new max sum is found, indices for max sum will be updated.

#### Solution
- Python

```python
class MaxSum3:
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        left, mid, right = 0, k, 2*k
        sum_l, sum_m, sum_r = sum(nums[left:left+k]), sum(nums[mid:mid+k]), sum(nums[right:right+k])
        max_l, max_m, max_r = sum_l, sum_l + sum_m, sum_l + sum_m + sum_r
        idx_l, idx_m, idx_r = left, [left, mid], [left, mid, right]
        while right < len(nums) - k:
            sum_l += (nums[left + k] - nums[left])
            sum_m += (nums[mid + k] - nums[mid])
            sum_r += (nums[right + k] - nums[right])
            if sum_l > max_l:
                max_l = sum_l
                idx_l = left + 1
            if max_l + sum_m > max_m:
                max_m = max_l + sum_m
                idx_m = [idx_l, mid + 1]
            if max_m + sum_r > max_r:
                max_r = max_m + sum_r
                idx_r = idx_m + [right + 1]
            left += 1
            mid += 1
            right += 1
        return idx_r
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer[]}
def max_sum_of_three_subarrays(nums, k)
  left, mid , right = 0, k, 2*k
  sum_l, sum_m, sum_r = nums[left, k].sum, nums[mid, k].sum, nums[right, k].sum
  max_l, max_m, max_r = sum_l, sum_l + sum_m, sum_l + sum_m + sum_r
  idx_l, idx_m, idx_r = left, [left, mid], [left, mid, right]
  while right < nums.size - k
    sum_l += (nums[left + k] - nums[left])
    sum_m += (nums[mid + k] - nums[mid])
    sum_r += (nums[right + k] - nums[right])
    if sum_l > max_l
      max_l = sum_l
      idx_l = left + 1
    end
    if max_l + sum_m > max_m
      max_m = max_l + sum_m
      idx_m = [idx_l, mid + 1]
    end
    if max_m + sum_r > max_r
      max_r = max_m + sum_r
      idx_r = idx_m + [right + 1]
    end
    left += 1
    mid += 1
    right += 1
  end
  idx_r
end
```

#### Complexity
- Time: O(n)
- Space: O(n)