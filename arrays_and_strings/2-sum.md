# 2 Sum

#### Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Example
Input: `nums = [2, 7, 11, 15]`, `target = 9`

Output: `[0, 1] - nums[0] + nums[1] = 2 + 7 = 9`

#### How to Solve

Use dictionary (Python, Hash in Ruby, Map in Java).
A key is `target - v`, and a value is index.
If the value in the given array is the key, return the
indices.

#### Solution

- Python

```python
def twoSum(nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    d = {}
    for i, v in enumerate(nums):
        if v in d:
            return [d[v], i]
        else:
            d[target-v] = i
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer[]}
def two_sum(nums, target)
  h = {}
  nums.each_with_index do |num, index|
    temp = target - num
    if h[temp]
      return [h[temp], index]
    else
      h[num] = index
    end
  end
end
```

#### Complexity
- Time: O(n)
- Space: O(n)
