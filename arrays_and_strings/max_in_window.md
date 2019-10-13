# Sliding Window Maximum

#### Description

Given an array of integers `nums` and sliding window size `k`, find the maximum value in each window when the window slides from the leftmost to rightmost one by one.

#### Example
Input: `nums = [1,3,-1,-3,5,3,6,7], and k = 3`

Output: `[3,3,5,5,6,7]`

Explanation:

```
window     max
[1,3,1]     3
[3,-1,-3]   3
[-1,-3,5]   5
[-3,5,3]    5
[5,3,6]     6
[3,6,7]     7
```

#### How to Solve

Start from the maximum value of the first window. When the window slides, three cases are there.

1. The comming value is greater than the current max.
2. The leaving value is the maximum value.
3. Neither of above.

The first case is easy, just add the in-coming value to the result. For the second case, considering multiple maximum values may or may not be in a previous window, find a new maximum in the window. The third case is another easy one. The in-coming value can't be a maximum, so add the last maximum to the result.

#### Solution
- Python

```python
class MaxInWindow:
    def maxSlidingWindow(self, nums: 'List[int]', k: int) -> 'List[int]':
        if not nums: return []
        if k == len(nums): return [max(nums)]
        result = [max(nums[:k])]
        for i in range(k, len(nums)):
            if nums[i] > result[-1]:
                result.append(nums[i])
            else:
                if nums[i-k] == result[-1]:
                    result.append(max(nums[i-k+1:i+1]))
                else:
                    result.append(result[-1])
        return result
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(1)`
