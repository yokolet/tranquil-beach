# Jump Game

#### Description

Give an array of non-negative integers, where each element represents maximum jump length at that index, find it is possible to reach to the last index. The starting index is always 0.

#### Example 1
Input: `[2,3,1,1,4]`

Output: True

Explanation: Jump to the index 1, then jump to the index 4 which is the last index.

#### Example 2
Input: `[3,2,1,0,4]`

Output: False

Explanation: All indices from 0 to 2 goes to the index 3, then can't go anywhere.

#### How to Solve

Start from the last index and memoize the previous index.
While iterating to the index 0, check `i + nums[i]`. This is the maximum reachable index. If the reachable index is greater than or equal to the previous index, update the previous. In the end, check the previous index becomes 0. 

#### Solution

- Python

```python
class JumpGame:
    def canJump(self, nums: 'List[int]') -> bool:
        n = len(nums)
        prev = n - 1
        for i in range(n-2, -1, -1):
            if i + nums[i] >= prev:
                prev = i
        return prev == 0
```

#### Complaxity
- Time: `O(n)` -- n is a length of a given array
- Space: `O(1)`
