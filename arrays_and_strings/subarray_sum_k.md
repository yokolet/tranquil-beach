# Subarray Sum Equals K

#### Description

Given an array of integers and a target value k, find the total number of continuous subarrays whose sum equals to k.

The length of the array is in range [1, 20,000].
The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

#### Example
Input: `nums = [1,1,1]`, `k = 2`

Output: 2

#### How to Solve

Use dictionary (Hash in Ruby) to save previous state.
The dictionary's key is an accumulated sum, and value is a count of that sum.

If the dictionary has a key "accumulated sum - k", add the value to the total count.

The loop is slightly different between Python and Ruby.
This comes from how the initial value is set.

#### Solution
- Python

```python
class SubarraySumK:
    def subarraySum(self, nums: 'List[int]', k: int) -> int:
        count, acc, memo = 0, 0, {0: 1}
        for v in nums:
            acc += v
            if acc - k in memo:
                count += memo[acc - k]
            if acc in memo:
                memo[acc] += 1
            else:
                memo[acc] = 1
        return count
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def subarray_sum(nums, k)
  count, acc, memo = 0, 0, Hash.new(0)
  nums.each do |v|
    acc += v
    count += 1 if acc == k
    count += memo[acc - k]
    memo[acc] += 1
  end
  count
end
```

#### Complexity
- Time: O(n)
- Space: O(n)