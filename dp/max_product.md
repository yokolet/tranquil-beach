# Maximum Product Subarray

#### Description

Given an array of integers, find the contiguous subarray which has the largest product. The largest subarray contains at least one element in the given array.

#### Example 1
Input: `[2,3,-2,4]`

Output: `6`

Explanation: `[2,3]` gives the largest product of `6`.

#### Example 2
Input: `[-2,0,-1]`

Output: `0`

#### How to Solve

The dynamic programming approach works to solve this problem. The input array may contain negative value, so the minimum value at that index may become maximum at the next index, for example, `-2 * -3`. Since the problem asks the contiguous subarray, keep tracking current maximum and minimum values. Then compare overall and current maximum values.

#### Solution
- Python

```python
class MaxProduct:
    def maxProduct(self, nums: 'List[int]') -> int:
        cur_min, cur_max, max_prod = nums[0], nums[0], nums[0]
        for v in nums[1:]:
            cur_min, cur_max = min(cur_min*v, cur_max*v, v), max(cur_min*v, cur_max*v, v)
            max_prod = max(max_prod, cur_max)
        return max_prod
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(1)`
