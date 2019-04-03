# Intersection of Two Arrays

#### Description

Given two arrays, write a function to compute their intersection.

Each element in the result must be unique.
The result can be in any order.

#### Example 1
Input: `nums1 = [1,2,2,1], nums2 = [2,2]`

Output: `[2]`

#### Example 2
Input: `nums1 = [4,9,5], nums2 = [9,4,9,8,4]`

Output: `[9,4]`

#### How to Solve

Create two sets from given two arrays, then take intersection of two.

#### Solution
- Python

```python
class Intersection:
    def intersection(self, nums1: 'List[int]', nums2: 'List[int]') -> 'List[int]':
        s1, s2 = set(nums1), set(nums2)
        return list(s1 & s2)
```

- Ruby

```ruby
# @param {Integer[]} nums1
# @param {Integer[]} nums2
# @return {Integer[]}
def intersection(nums1, nums2)
  (Set.new(nums1) & Set.new(nums2)).to_a
end
```

#### Complexity
- Time: O(m+n) -- m,n are lengths of nums1, nums2
- Space: O(m+n)