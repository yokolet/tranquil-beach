# Search in Rotated Sorted Array with Duplicates

#### Description

Given an array of sorted in ascending order and target value,
return true if the target value exists. Return false if the target value doesn't exist.

The given sorted array may or may not be rotated at some unknown pivot. The array may have duplicated values, for example, [2,5,6,0,0,1,2].

#### Example 1
Input: `nums = [2,5,6,0,0,1,2]`, `target = 0`

Output: true

#### Example 2
Input: `nums = [2,5,6,0,0,1,2]`, `target = 3`

Output: false

#### How to Solve

This is a binary search problem with two twists.
Since the array may be rotated, compare low, high and mid values with the target to decide what half should be looked at next.
Additionally, the given array may have duplicates, so compare low and mid values. If those are the same, increment low.

#### Solution
- Python

```python
class RotatedSortedArrayWithDup:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """
        if not nums: return False
        n = len(nums)
        low, high = 0, n - 1
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] == target: return True
            if nums[mid] == nums[low]:
                low += 1
            elif nums[low] < nums[mid]:
                if nums[low] <= target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            elif nums[mid] <= nums[high]:
                if nums[mid] < target <=nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
        return False
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} target
# @return {Boolean}
def search(nums, target)
  return false if nums.nil? || nums.empty?
  n = nums.size
  low, high = 0, n - 1
  while low <= high
    mid = (low + high) / 2
    return true if nums[mid] == target
    if nums[mid] == nums[low]
      low += 1
    elsif nums[low] < nums[mid]
      if nums[low] <= target && target < nums[mid]
        high = mid - 1
      else
        low = mid + 1
      end
    elsif nums[mid] <= nums[high]
      if nums[mid] < target && target <= nums[high]
        low = mid + 1
      else
        high = mid - 1
      end
    end
  end
  false
end
```

#### Complexity
- Time: O(log(n))
- Space: O(1)