# Intersection of Two Arrays with Duplicates

#### Description

Given two arrays of integers, find their intersection.
Each element in the result should appear as many times as it shows in both arrays.

The result can be in any order.

#### Example 1
Input: `nums1 = [1,2,2,1]`, `nums2 = [2,2]`

Output: `[2,2]`

#### Example 2
Input: `nums1 = [4,9,5]`, `nums2 = [9,4,9,8,4]`

Output: `[4,9]`

#### How to Solve

Use dictionary (Hash in Ruby) to save counts of the longer array. While iterating the shorter array, check if the element exists in the counts map. If the counts of the digit is greater than zero, add the element to the result and descrement.

#### Solution
- Python

```python
from collections import defaultdict

class TwoArrays:
    def intersect(self, nums1: 'List[int]', nums2: 'List[int]') -> 'List[int]':
        memo, result = defaultdict(int), []
        if len(nums2) > len(nums1):
            nums1, nums2 = nums2, nums1
        for v in nums1:
            memo[v] += 1
        for v in nums2:
            if v in memo and memo[v] > 0:
                result.append(v)
                memo[v] -= 1
        return result
```

- Ruby

```ruby
# @param {Integer[]} nums1
# @param {Integer[]} nums2
# @return {Integer[]}
def intersect(nums1, nums2)
  if nums1.size < nums2.size
    nums1, nums2 = nums2, nums1
  end
  memo, result = {}, []
  memo.default = 0
  nums1.each { |v| memo[v] += 1 }
  nums2.each do |v|
    if memo.has_key?(v) && memo[v] > 0
      result << v
      memo[v] -= 1
    end
  end
  result
end
```

#### Complexity
- Time: `O(m+n)` - m, n are the lengths of two arrays
- Space: `O(n)` - n is a longer length of two arrays.
