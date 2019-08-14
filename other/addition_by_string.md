# Add Strings

#### Description

Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

The length of both num1 and num2 is < 5100.
Both num1 and num2 contains only digits 0-9.
Both num1 and num2 does not contain any leading zero.
You must not use any built-in BigInteger library or convert the inputs to integer directly.

#### Example 1
Input: `num1 = "999", num2 = "1"`

Output: `"1000"`

#### Example 2
Input: `num1 = "1", num2 = "12345"`

Output = "12346"

#### How to Solve

Start from the right most elements of num1, num1 and go over to the left.
Using carry, add up one by one.

#### Solution
- Python

```python
class AdditionByString:
    def addStrings(self, num1: str, num2: str) -> str:
        i, j, carry, result = len(num1) - 1, len(num2) - 1, 0, ""
        while i >= 0 or j >= 0 or carry > 0:
            v_1 = int(num1[i]) if i >= 0 else 0
            v_2 = int(num2[j]) if j >= 0 else 0
            carry, v = divmod(carry + v_1 + v_2, 10)
            result = str(v) + result
            i -= 1
            j -= 1
        return result
```

- Ruby

```ruby
# @param {String} num1
# @param {String} num2
# @return {String}
def add_strings(num1, num2)
  i, j, carry, result = num1.size - 1, num2.size - 1, 0, ""
  while i >=0 || j >= 0 || carry > 0
    if i >= 0
      carry += num1[i].to_i
    end
    if j >= 0
      carry += num2[j].to_i
    end
    carry, v = carry.divmod(10)
    result = v.to_s + result
    i -= 1
    j -= 1
  end
  result
end
```

#### Complexity
- Time: `O(n)` -- n is longer length of num1 or num2
- Space: `O(1)`