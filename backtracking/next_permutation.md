# Next Permutation

#### Description

Given an array of integers, rearrange integers into the lexicographically next greater permutation. If such arrangement is not possible, rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

#### Example 1
Input: `[1, 2, 3]`

Rearranged: `[1. 3. 2]`

#### Example 2
Input: `[3, 2, 1]`

Rearranged: `[1, 2, 3]`

#### Example 3
Input: `[1, 1, 5]`

Rearranged: `[1, 5, 1]`

#### How to Solve

The solution uses the algorithm, [next lexicographical permutation](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm). This algorithm finds lexicographically one bigger permutation.

The algorithm takes steps below:

1. find longest non-increasing suffix such that `array[index] < array[index + 1]`
2. find a pivot index such that the first `array[index] > array[index + 1]`
3. find a ceil (successor) such that `array[pivot] < array[succ]`
4. swap pivot and successor, `array[pivot], array[succ]`
5. reverse suffix from `array[pivot + 1]` to the end

#### Solution
- Python

```python
class NextPermutation:
    def nextPermutation(self, nums: 'List[int]') -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        i = n - 2
        while i >= 0:
            if nums[i] < nums[i + 1]: break
            i -= 1
        if i == -1:
            nums[:] = nums[::-1]
        else:
            succ = n - 1
            while nums[succ] <= nums[i]:
                succ -= 1
            nums[i], nums[succ] = nums[succ], nums[i]
            nums[i+1:] = nums[i+1:][::-1]
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Void} Do not return anything, modify nums in-place instead.
def next_permutation(nums)
  n = nums.size
  i = n - 2
  while i >= 0
    break if nums[i] < nums[i + 1]
    i -= 1
  end
  if i == -1
    nums.sort!
  else
    succ = n - 1
    while nums[succ] <= nums[i]
      succ -= 1
    end
    nums[i], nums[succ] = nums[succ], nums[i]
    nums[i+1..-1] = nums[i+1..-1].reverse
  end
end
```

#### Complexity
- Time: O(n) (O(nlog(n)) -- if the given array is the greatest)
- Space: O(1)