# Subsets

#### Description

Given a set of distinct integers, nums, return all possible subsets (the power set).

The solution set must not contain duplicate subsets.

#### Example
Input: `nums = [1,2,3]`

Output:
```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

#### How to Solve

In general, the solution uses a combination of binary numbers.
However, the solution here takes step by step approach. The result goes like this:

```
[[]]
[[], [1]]
[[], [1], [2], [1, 2]]
[[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]
```

In each iteration, an element from given array is mapped to each element in the array, which will be added up to the previous array.

#### Solution
- Python

```python
from functools import reduce

class Subsets:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        return reduce(lambda acc, x: acc + [y + [x] for y in acc], nums, [[]])
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def subsets(nums)
  nums.reduce([[]]) { |acc, x| acc + acc.map { |y| y + [x]}}
end
```

#### Complexity
- Time: O(n^2)
- Space: O(2^n)