# 2 Sum

### Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example
Input: `nums = [2, 7, 11, 15]`, `target = 9`

Output: `[0, 1] - nums[0] + nums[1] = 2 + 7 = 9`

{% code-tabs %}

{% code-tabs-item title=undefined %}
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
{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}
```ruby
puts "Hello World!"
```
{% endcode-tabs-item %}

{% endcode-tabs %}
