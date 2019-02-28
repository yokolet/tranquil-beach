# Search in Rotated Sorted Array

#### Description

Given an array of sorted in ascending order and target value,
find the index of the target value. Return -1 if the target value doesn't exist.

The given sorted array may or may not be rotated at some unknown pivot, for example, [4,5,6,7,0,1,2].

No duplicate exists in the given array.
The algorithm should run in O(log(n)).

#### Example 1
Input: `nums = [4,5,6,7,0,1,2]`, `target = 0`

Output: 4

#### Example 2
Input: `nums = [4,5,6,7,0,1,2]`, `target = 3`

Output: -1

#### How to Solve

Do binary search. However, extra value checks are needed since the array may or may not be rotated.
If it is rotated, `nums[low]` may be greater than `nums[mid]`.
Checking values on the both ends and mid, next move will be chosen.

#### Solution
- Python

```python
class RotatedSortedArray:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums: return -1
        n = len(nums)
        low, high = 0, n - 1
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] == target: return mid
            if nums[low] <= nums[mid]:
                if nums[low] <= target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] < target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
        return -1
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer}
def search(nums, target)
  return -1 if nums.nil? || nums.empty?
  low, high = 0, nums.size - 1
  while low <= high
    mid = (low + high) / 2
    return mid if nums[mid] == target
    if nums[low] <= nums[mid]
      if nums[low] <= target && target < nums[mid]
        high = mid - 1
      else
        low = mid + 1
      end
    else
      if nums[mid] < target && target <= nums[high]
        low = mid + 1
      else
        high = mid - 1
      end
    end
  end
  return -1
end
```

#### Complexity
- Time: O(log(n))
- Space: O(1)