# Split Array into Consecutive Subsequences

#### Description

Given an array of integers, sorted in ascending order, return `True` if and only if the array can be split into 1 or more subsequences such that each subsequences consists of consecutive integers and has length at least 3.

#### Example 1

Input: `[1,2,3,3,4,5]`

Output: `True`

Explanation: `[1,2,3], [3,4,5]`

#### Example 2

Input: `[1,2,3,3,4,4,5,5]`

Output: `True`

Explanation: `[1,2,3,4,5], [3,4,5]`

#### Example 3

Input: `[1,2,3,4,4,5]`

Output: `False`

Explanation: `[1,2,3,4,5], [4]` or `[1,2,3,4],[4,5]`

#### How to Solve

A new element, `x`, can be added to an existing group when the last element of the group is `x - 1`. If not, the new element can create a new group when `x+1` and `x+2` are left more than one. Both conditions are not met, the result is `False`.

To check two conditions, use two dictionlaries to keep elements left and the last elements. When all elements in the given array are checked, the result is `True`

Similar Problem:
- [Divide Array in Sets of K Consecutive Numbers](consecutive_k_numbers.md)

#### Solution
- Python

```python
from collections import defaultdict

class ConsecutiveSubsequences:
    def isPossible(self, nums: 'List[int]') -> bool:
        num_dict = defaultdict(int)
        for i in range(len(nums)):
            num_dict[nums[i]] += 1
        last_dict = defaultdict(int)
        for num in nums:
            if last_dict[num-1]:
                last_dict[num-1] -= 1
            elif num_dict[num+1] and num_dict[num+2]:
                num_dict[num+1] -= 1
                num_dict[num+2] -= 1
            else:
                return False
            last_dict[num] += 1
        return True
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(n)`
