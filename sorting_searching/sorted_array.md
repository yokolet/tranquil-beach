# Merge Two Sorted Arrays

#### Description

Given two sorted integer arrays, nums1 and nums2, merge nums2 into nums1 as one sorted array.

The number of elements initialized in nums1 and nums2 are m and n respectively.
Assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.

#### Example
Input:
```
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3
```

Output: `[1,2,2,3,5,6]`

#### How to Solve

Fill num1 from the index, `m + n -1`. While filling out the array, decrement m or n. In the end of the loop, m or n may not zero. If m is not zero, leave it as is. If n is not zero, fill the first n elements by values of nums2.

#### Solution
- Python

```python
class SortedArray:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        while m > 0 and n > 0:
            if nums1[m - 1] >= nums2[n - 1]:
                nums1[m + n - 1] = nums1[m - 1]
                m -= 1
            else:
                nums1[m + n - 1] = nums2[n - 1]
                n -= 1
        if n > 0:
            for i in range(n):
                nums1[i] = nums2[i]
```

- Ruby

```ruby
# @param {Integer[]} nums1
# @param {Integer} m
# @param {Integer[]} nums2
# @param {Integer} n
# @return {Void} Do not return anything, modify nums1 in-place instead.
def merge(nums1, m, nums2, n)
  while m > 0 && n > 0
    if nums1[m - 1] >= nums2[n - 1]
      nums1[m + n - 1] = nums1[m - 1]
      m -= 1
    else
      nums1[m + n - 1] = nums2[n - 1]
      n -= 1
    end
  end
  if n > 0
    (0...n).each { |i| nums1[i] = nums2[i] }
  end
end
```

#### Complexity
- Time: `O(n+m)` -- m and n are the lengths of given arrays, `m > n`
- Space: `O(m)`