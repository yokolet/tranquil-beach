# Contiguous Subarray

#### Description

Given a binary array, find the maximum length of contiguous subarray with equal number of 0 and 1.

#### Example 1

Input: `[0,1]`

Output: `2`

#### Example 2

Input: `[0,1,0]`

Output: `2`

Explanation: `[0,1]` or `[1,0]` is the longest contiguous subarray with equal number of 0 and 1.

#### How to Solve

A subarray sum and indices matter to solve this problem. This suggests to use a dictionary (map). The key is the sum to index `i` and the value is the index `i`. If the same sum exists in the dictionary, it won't update the index since the problem asks the longest. If the same sum exists, check the length from that index to current and compare to the max_length so far.

In this problem, how to calcuate the sum is the key to solve the problem. The solution here considers 0 as the value, -1 and sums up.

Similar problems:
- [Maximum Size Subarray Sum Equals k](max_subarray_sum_k.md)

#### Solution
- Python

```python
class LongestBinarySubarray:
    def findMaxLength(self, nums: 'List[int]') -> int:
        max_len, count, diff = 0, 0, {0: -1}
        for i in range(len(nums)):
            count += 1 if nums[i] == 1 else -1
            if count in diff:
                max_len = max(max_len, i - diff[count])
            else:
                diff[count] = i
        return max_len
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(n)`
