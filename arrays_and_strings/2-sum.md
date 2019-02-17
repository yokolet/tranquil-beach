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

#### Complexity

- Time: O(n)
- Space: O(n)

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
{% endcode-tabs-item %}

{% code-tabs-item title="Java" %}
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        if (nums == null || nums.length == 0) { return result; }
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < nums.length; i++) {
            int temp = target - nums[i];
            if (map.containsKey(temp)) {
                result[0] = map.get(temp);
                result[1] = i;
                return result;
            } else {
                map.put(nums[i], i);
            }
        }
        return result;
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
