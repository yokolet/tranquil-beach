# Product of Array Except Self

#### Description

Given an array of n integers where n > 1, return an array such that output[i] is equal to the product of all the elements of given array except nums[i].

#### Example
Input:  `[1,2,3,4]`

Output: `[24,12,8,6]`

#### How to Solve

Iterate the given array twice. The first step computes `1, 1 * X0, 1 * X0 * X1, 1 * X0 * X1 * X2...` The second step goes from the end to 0 while computing, `Rn * 1, Rn-1 * 1 * Xn, Rn-2 * 1 * Xn * Xn-1, Rn-3 * 1 * Xn * Xn-1 * Xn-2,...`, where Ri denotes ith element of the array created at the first step.

#### Solution
- Python

```python
class Product:
    def productExceptSelf(self, nums: 'List[int]') -> 'List[int]':
        if not nums: return []
        acc, result = 1, []
        for n in nums:
            result.append(acc)
            acc *= n
        acc = 1
        for i in range(len(nums)-1, -1, -1):
            result[i] *= acc
            acc *= nums[i]
        return result
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[]}
def product_except_self(nums)
  return [] if nums.nil? || nums.empty?
  acc, result = 1, []
  nums.each do |n|
    result << acc
    acc *= n
  end
  acc = 1
  (nums.size - 1).downto(0) do |i|
    result[i] *= acc
    acc *= nums[i]
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(1)
