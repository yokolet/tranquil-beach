# Minimum Step Jump Game

#### Description

Give an array of non-negative integers, where each element represents maximum jump length at that index, find the minimum steps to reach to the last index. The starting index is always 0. The last index is always reachable.

#### Example
Input: `[2,3,1,1,4]`

Output: `2`

Explanation: The minimum steps are jumping to index 1, then the 4 which is the last index.

#### How to Solve

This problem asks to find minimum jumps, so start from index 0 and keep tracking the current index (like left pointer). While iterating the given array, check if the index exeeds the current index. If so, it needs a jump. Count up steps and replace the current index with the maximum possible jump at that index.

#### Solution

- Python

```python
class MinJumpGame:
    def jump(self, nums: 'List[int]') -> int:
        if not nums or len(nums) < 2: return 0
        steps, cur, next = 0, 0, 0
        for i in range(len(nums)):
            if i > cur:
                steps += 1
                cur = next
            next = max(next, i+nums[i])
        return steps
```

#### Complexity
- Time: `O(n)` -- n is a length of the given list
- Space: `O(1)`
