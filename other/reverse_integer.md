# Reverse Integer

#### Description

Given a 32-bit signed integer, reverse digits of an integer.

Assume the environment could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. Return 0 when the reversed integer overflows.

#### Example 1
Input: `123`

Output: `321`

#### Example 2
Input: `-123`

Output: `-321`

#### Example 3
Input: `120`

Output: `21`

#### How to Solve

Save sign and iterate from the left (ones place) to right.
The given integer modulo 10 is added up to the `result * 10`, while a quotient goes to the next round.

In the end, the result should be checked whether it is overflowed or not.


#### Solution
- Python

```python
class ReverseInteger:
    def reverse(self, x: int) -> int:
        result = 0
        sign = -1 if x < 0 else 1
        v = abs(x)
        while v > 0:
            v, rem = divmod(v, 10)
            result = result * 10 + rem
        result *= sign
        return result if result in range(-2**31, 2**31-1) else 0
```

- Ruby

```ruby
# @param {Integer} x
# @return {Integer}
def reverse(x)
  sign = x < 0 ? -1 : 1
  v = x.abs
  result = 0
  while v > 0
    v, rem = v.divmod(10)
    result = result * 10 + rem
  end
  result *= sign
  result < -2**31 || result > (2**31-1) ? 0 : result
end
```

#### Complexity
- Time: `O(n)` -- n is a length of the givien digits
- Space: `O(1)`