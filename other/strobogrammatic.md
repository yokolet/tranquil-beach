# Strobogrammatic Number

#### Description

Given a number as a string, determine if a number is strobogrammatic.

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

#### Example 1
Input: `"69"`

Output: `True`

#### Example 2
Input: `"88"`

Output: `True`

#### Example 3
Input: `"962"`

Output: `False`

#### How to Solve

Use two pointers, left and right. If character on the left and right are the strobogrammatic number pair, move pointers. Otherwise, return false.

To quickly identify the strobogrammatic number or not, the solution here uses a dictionary (Hash in Ruby).

#### Solution
- Python

```python
class Strobogrammatic:
    def isStrobogrammatic(self, num: str) -> bool:
        memo = {'0': '0', '1': '1', '6': '9', '8': '8', '9': '6'}
        left, right = 0, len(num) - 1
        while left <= right:
            if num[left] not in memo and num[right] not in memo: return False
            if memo[num[left]] != num[right]: return False
            left += 1
            right -= 1
        return True
```

- Ruby

```ruby
# @param {String} num
# @return {Boolean}
def is_strobogrammatic(num)
  memo = {'0' => '0', '1' => '1', '6' => '9', '8' => '8', '9' => '6'}
  left, right = 0, num.size - 1
  while left <= right
    return false if !memo.has_key?(num[left]) && !memo.has_key?(num[right])
    return false if memo[num[left]] != num[right]
    left += 1
    right -= 1
  end
  true
end
```

#### Complexity
- Time: O(n)
- Space: O(1)