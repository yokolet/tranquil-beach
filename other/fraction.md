# Fraction to Recurring Decimal

#### Description

Given two integers, numerator and denominator of a fraction, return the fraction in a string format. If the fractional part consists of repeating digits, enclose the repeating part in parentheses.

#### Example 1

Input: `numerator = 1, denominator = 2`

Output: `"0.5"`

#### Example 2

Input: `numerator = 2, denominator = 1`

Output: `"2"`

#### Example 3

Input: `numerator = 2, denominator = 3`

Output: `"0.(6)"`

#### How to Solve

First create a string for the integer part. Then move on to processing a fracutional part. Start from a modulo. If the modulo is 0, return the string. To find a repeating digits, a dictionary is a useful data structure. Save the modulo and the string length so far to insert a staring parenthesis later. When the modulo found in the dictionary, get the string length at the previous same modulo. Insert '(' and append ')' at the end. The solution here may add '(0)', so it is removed.

#### Solution

- Python

```python
class Fraction:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        if numerator == 0: return '0'
        result = ''
        if numerator * denominator < 0: result += '-'
        n, d = abs(numerator), abs(denominator)
        result += str(n // d)

        r = n % d
        if r == 0: return result

        result += '.'
        memo = {}
        while r not in memo:
            memo[r] = len(result)
            result += str(r * 10 // d)
            r =  r * 10 % d
        result = result[:memo[r]] + '(' + result[memo[r]:] + ')'
        return result.replace('(0)', '')
```

#### Complexity

- Time: O(d) -- d is a length of repeating digits
- Space: O(d)