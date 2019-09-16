# Plus One

#### Description

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

The given array doesn't have any leading zero except `[0]`.

#### Example 1
Input: `[1,2,3]`

Output: `[1,2,4]`

#### Example 2
Input: `[4,3,2,1]`

Output: `[4,3,2,2]`

#### How to Solve

Traverse the given array from back to front. If the digit is not 9, just add one and return the array. If the digit is 9, update it to 0 then go next digit. All digits are checked and still it doesn't return, which is the case, 1000... (0 continues the length of digits).

Note: In Ruby code, `[1] + Array.new(digits.size, 0)` is much faster than `[1] + digits`. However, Python's `[1] + digits` runs faster than `[1] + [0]*len(digits)`. Because of this, Ruby's space complexity is O(n) if the result's space is counted.

#### Solution
- Python

```python
class PlusOne:
    def plusOne(self, digits: 'List[int]') -> 'List[int]':
        for i in range(len(digits) - 1, -1, -1):
            if digits[i] != 9:
                digits[i] += 1
                return digits
            digits[i] = 0
        return [1] + digits
```

- Ruby

```ruby
# @param {Integer[]} digits
# @return {Integer[]}
def plus_one(digits)
  (digits.size-1).downto(0) do |i|
    if digits[i] != 9
      digits[i] += 1
      return digits
    else
      digits[i] = 0
    end
  end
  [1] + Array.new(digits.size, 0)
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(1)`
