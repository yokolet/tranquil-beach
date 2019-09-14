# Longest Continuous Increasing Subsequence

#### Description

Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).

#### Example 1
Input: `[1,3,5,4,7]`

Output: `3`

Explanation: `[1,3,5]` is the longest, and its length is 3. 

#### Example 2
Input: `[2,2,2,2,2]`

Output: `1`

Explanation: [2] is the longest, and its length is 1. 

#### How to Solve

Compare current and previous values in the given array. If the current is greater than previous, increment a length so far. If not, update max length comparing max length and length. Then, set the length so far to 1. In the end, compare max lenght and length so far since the array may end with a greater value.

#### Solution
- Python

```python
class Lcis:
    def findLengthOfLCIS(self, nums: 'List[int]') -> int:
        if not nums: return 0
        max_len, length, prev = 1, 1, nums[0]
        for cur in nums[1:]:
            if prev < cur:
                length += 1
            else:
                max_len = max(max_len, length)
                length = 1
            prev = cur
        return max(max_len, length)
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def find_length_of_lcis(nums)
  return 0 if nums.nil? || nums.empty?
  max_length, length, prev = 1, 1, nums[0]
  (1...nums.length).each do |i|
    if prev < nums[i]
      length += 1
    else
      max_length = [max_length, length].max
      length = 1
    end
    prev = nums[i]
  end
  [max_length, length].max
end
```

#### Complexity
- Time: O(n)
- Space: O(1)