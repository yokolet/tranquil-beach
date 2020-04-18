# Divide Array in Sets of K Consecutive Numbers

#### Description

Given an array of integers and positive integer, `k`, determine whether it is possible to divide the array into sets of `k` consecutive numbers. Return `True` if it is possible, otherwise return `False`.

#### Example 1

Input: `nums = [1,2,3,3,4,4,5,6], k = 4`

Output: `True`

Explanation: `[1,2,3,4]` and `[3,4,5,6]`

#### Example 2

Input: `nums = [3,2,1,2,3,4,3,4,5,9,10,11], k = 3`

Output: `True`

Explanation: `[1,2,3]`, `[2,3,4]`, `[3,4,5]` and `[9,10,11]`

#### Example 3

Input: `nums = [1,2,3,4], k = 3`

Output: `False`

Explanation: The given array is unable to divide in subarrays of length 3.

#### Example 4

Input: `nums = [1,3,4,6], k = 4`

Output: `False`

Explanation: The given array is unable to create a consecutive subarray of length 4.

#### How to Solve

The given array size should be a multiple of k. If not, return false.
Then, count each value. Since the values should be consecutive, check counts of consecutive k values. If those values are greater than starting value's count, check next.

Similar problem:
- [Split Array into Consecutive Subsequences](consecutive_subsequences.md)

#### Solution
- Python

```python
from collections import defaultdict

class ConsecutiveKNumbers:
    def isPossibleDivide(self, nums: 'List[int]', k: int) -> bool:
        if len(nums) % k != 0: return False
        counts = defaultdict(int)
        for i in range(len(nums)):
            counts[nums[i]] += 1
        for v in sorted(counts):
            if counts[v] == 0: continue
            count = counts[v]
            for i in range(k):
                if v+i in counts and counts[v+i] - count >= 0:
                    counts[v+i] -= count
                else:
                    return False
        return True
```

#### Complexity
- Time: `O(knlog(n))` -- k, n are a size of subarray and length of the given array respectively
- Space: `O(m)` -- m is a number of distinct values of the given array
