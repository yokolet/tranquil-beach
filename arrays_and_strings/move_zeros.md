# Move Zeros

#### Description

Given an array of integers, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

This must be done by in-place without making a copy of the array.
Minimize the total number of operations.

#### Example
Input: `[0,1,0,3,12]`

Result: `[1,3,12,0,0]` -- no output, input array in the end

#### How to Solve

Keep track the left most index of zero. While iterating the array, if a current value is non-zero, swap it with the left most position's zero. Then, incremenet the left most index of zero.

#### Solution
- Python

```python
class MoveZeros:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        zero = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[i], nums[zero] = nums[zero], nums[i]
                zero += 1
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Void} Do not return anything, modify nums in-place instead.
def move_zeroes(nums)
  zero = 0
  (0...nums.size).each do |i|
    if nums[i] != 0
      nums[i], nums[zero] = nums[zero], nums[i]
      zero += 1
    end
  end
end
```

#### Complexity
- Time: O(n)
- Space: O(1)