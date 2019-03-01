# Unique Permutations with Duplicates

#### Description

Given an array of integers that might contain duplicates, find all possible unique permutations.

#### Example
Input: `[1,1,2]`

Output:
```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

#### How to Solve

A straightforward solution might be by recursive one.
However, it runs slow since it is a O(n!) algorithm.

The solution here uses the algorithm, [next lexicographical permutation](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm). This algorithm finds lexicographically one bigger permutation. Applying this algorithm one by one to a sorted array, it finds all unique permutations.

The algorithm takes steps below:

1. sort given array
2. find longest non-increasing suffix such that `array[index] < array[index + 1]`
3. find a pivot index such that the first `array[index] > array[index + 1]`
4. find a ceil (successor) such that `array[pivot] < array[succ]`
5. swap pivot and successor, `array[pivot], array[succ]`
6. sort suffix from `array[pivot + 1]` to the end


#### Solution
- Python

```python
class PermutationsWithDup:
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        n = len(nums)
        done = False
        result = []
        nums.sort()
        while not done:
            result.append(nums[:])
            i = n - 2
            while i >= 0:
                if nums[i] < nums[i + 1]: break
                i -= 1
            if i == -1: done = True
            else:
                succ = n - 1
                while nums[succ] <= nums[i]:
                    succ -= 1
                nums[i], nums[succ] = nums[succ], nums[i]
                nums[i+1:] = sorted(nums[i+1:])
        return result
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def permute_unique(nums)
  n = nums.size
  done = false
  result = []
  nums.sort!
  while !done
    result << nums.dup
    i = n - 2
    while i >= 0
      break if nums[i] < nums[i + 1]
      i -= 1
    end
    if i == -1
      done = true
    else
      succ = n - 1
      while nums[succ] <= nums[i]
        succ -= 1
      end
      nums[i], nums[succ] = nums[succ], nums[i]
      nums[i+1..-1] = nums[i+1..-1].sort!
    end
  end
  result
end
```

#### Complexity
- Time: O(nlog(n))
- Space: O(n!)