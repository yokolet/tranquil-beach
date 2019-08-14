# Find Peak Element

#### Description

Given an arry of integers, num, where nums[i] ≠ nums[i+1], find a peak element and return its index.

A peak element is an element that is greater than its neighbors.
The array may contain multiple peaks. In such a case, return the index to any one of the peaks.

Assume `nums[-1] = nums[n] = -∞`.

The algorithm should run in O(log(n)).

#### Example 1
Input: `nums = [1,2,3,1]`

Output: `2` (the index of `3` in the array)

#### Example 2
Input: `nums = [1,2,1,3,5,6,4]`

Output: `1 or 5 `

Explanation: the value 2 (index 1) or value 6 (index 5)

#### How to Solve

The problem says the solution should run in O(log(n)), binary search should be used.

The patterns of array is:
- always increases
- always decreases
- a peak exists

Given that, compare `nums[mid]` and `nums[mid+1]`. If the array value at mid is greater than mid+1, the peak should exist in the left half. Otherwise, the peak should exist in the right half.
In the end, left and right point the peak value.

#### Solution
- Python

```python
class PeakElement:
    def findPeakElement(self, nums: 'List[int]') -> int:
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[mid + 1]:
                right = mid
            else:
                left = mid + 1
        return left
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def find_peak_element(nums)
  left, right = 0, nums.size-1
  while left < right
    mid = (left + right) / 2
    if nums[mid] > nums[mid+1]
      right = mid
    else
      left = mid + 1
    end
  end
  left
end
```

#### Complexity
- Time: `O(log(n))`
- Space: `O(1)`