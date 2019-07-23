# Maximum Subarray

#### Description

Given an array of integers, find the contiguous subarray which has the largest sum. The largest subarray contains at least one element in the given array.

#### Example

Input: `[-2,1,-3,4,-1,2,1,-5,4]`

Output: `6`

Explanation: subarray `[4,-1,2,1]` gives the largest sum of 6.

#### How to Solve

The dynamic programming approach works here. Since the problem asks the contiguous subarray, compare which one is larger -- the current value or current value plus sum to previous value. Then, the larger value will be compared to the max value at that index. When all elements in the array are checked, the max value will be found.

#### Solution

- Python

```python
class MaxSubarray:
    def maxSubArray(self, nums: 'List[int') -> int:
        max_sum = float('-inf')
        cur_sum = 0
        for v in nums:
            cur_sum = max(cur_sum + v, v)
            max_sum = max(max_sum, cur_sum)
        return max_sum
```

#### Complexity

- Time: O(n)
- Space: O(1)