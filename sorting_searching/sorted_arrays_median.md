# Median of Two Sorted Arrays

#### Description

Given two sorted arrays, nums1 and nums2, whose lengths are m and n respectively, find the median of the two sorted arrays.

The time complexity should be O(log(m+n)).

#### Example 1

Input: `nums1 = [1, 3], nums2 = [2]`

Output: `2.0`

#### Example 2

Input: `nums1 = [1, 2], nums2 = [3, 4]`

Output: `2.5`

#### How to Solve

An easy solution is: merge two arrays, sort then return the middle value(s).

However, the requirement of this problem is O(log(n)), which means the binary search should be used.

The binary search indices will be based on the shorter array. First, the code focuses on the shorter array's index, `(low + high) // 2`, and the longer array's index, `(m + n + 1) // 2 - i`. Next, the indices to compare will be four of following.

- nums1's middle 2 indices -- `i - 1`(left1) and `i`(right1)
- nums2's muddle 2 indices -- `j - 1`(left2) and `j`(right2)

When `left1 > right2`, the median exists on the left half of nums1. So, `high` will be decreased. When `left2 > right1`, the median exists on the right half of nums1. So, `low` will be increased. Otherwise, the values for median were found. So, calculate and return the median.

#### Solution

- Python

```python
class SotredArraysMedian:
    def findMedianSortedArrays(self, nums1: 'List[int]', nums2: 'List[int]') -> float:
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
        m, n = len(nums1), len(nums2)
        if m == 0:
            return (nums2[(n - 1) // 2] + nums2[n // 2]) / 2
        
        low, high = 0, m
        while low <= high:
            i = (low + high) // 2
            j = (m + n + 1) // 2 - i
            left1 = nums1[i-1] if i > 0 else float('-inf')
            right1 = nums1[i] if i < m else float('inf')
            left2 = nums2[j-1] if j > 0 else float('-inf')
            right2 = nums2[j] if j < n else float('inf')
            if left1 > right2:
                high = i - 1
            elif left2 > right1:
                low = i + 1
            else:
                if (m + n) % 2 == 1:
                    return max(left1, left2)
                else:
                    return (max(left1, left2) + min(right1, right2)) / 2
```

#### Complexity

- Time: `O(log(n))`
- Space: `O(1)`