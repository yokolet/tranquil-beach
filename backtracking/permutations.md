# Permutations

#### Description

Given an array of distinct integers, find all possible permutations.

#### Example
Input: `[1,2,3]`

Output:

```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### How to Solve

Both Python and Ruby has built in function to generate permutations. If not, recursive solution with backtracking is the way to find it.

#### Solution
- Python

```python
from itertools import permutations

class Permutations:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        return [list(x) for x in permutations(nums)]
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def permute(nums)
  nums.permutation.to_a
end
```

#### Complexity
- Time: O(n!)
- Space: O(n!)