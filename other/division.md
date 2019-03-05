# Divide Two Integers

#### Description

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.
Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero.

#### Example 1
Input: `dividend = 10`, `divisor = 3`

Output: `3`

#### Example 2
Input: `dividend = 7`, `divisor = -3`

Output: `-2`

#### Example 3
Input: `dividend = -2147483648`, `divisor = -1`

Output: `2147483647`

#### How to Solve

Think in a binary way. All numbers are expressed by:

```
X = x_0 * (2 ^ 0) + x_1 * (2 ^ 1) + x_2 * (2 ^ 2) + ..... + x_n * (2 ^ n)
```

The first example is a division of:

```
devidend: 10 = 1010
divisor: 3 = 11


         1 1      <- quotient
    ---------
1 1) 1 0 1 0
       1 1
    ---------
       1 0 0
         1 1
    ---------
           1      <-- remainder
```

Actual calculation starts from subtracting `11`. Then the divisor is shifted 1 bit left -- `110`, and used to the next subtraction.

#### Solution
- Python

```python
class Division:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        if (dividend > 0 and divisor > 0) or\
            (dividend < 0 and divisor < 0):
            sign = 1
        else:
            sign = -1
        n, d = abs(dividend), abs(divisor)
        result = 0
        while d <= n:
            tmp, count = d, 1
            while tmp <= n:
                n -= tmp
                result += count
                count <<= 1
                tmp <<= 1
        result *= sign
        return min(max(-2**31, result), 2**31 - 1)
```

- Ruby

```ruby
# @param {Integer} dividend
# @param {Integer} divisor
# @return {Integer}
def divide(dividend, divisor)
  if (dividend >= 0 and divisor >= 0) or (dividend < 0 
    sign = 1
  else
    sign = -1
  end
  n, d = dividend.abs, divisor.abs
  result = 0
  while d <= n
    tmp, count = d, 1
    while tmp <= n
      n -= tmp
      result += count
      count <<= 1
      tmp <<= 1
    end
  end
  result *= sign
  [[-2**31, result].max, 2**31 - 1].min
end
```

#### Complexity
- Time: O(log(n))
- Space: O(1)