#### Multiply Strings

#### Description

Given two strings representing non-negative integers, return the product of two numbers as a string. The solution must not use any built-in BigInteger library or convert the inputs to integer directly.

The two numbers do not contain any leading zero, expect 0 itself.

#### Example 1

Input: `num1 = "2", num2 = "3"`

Output: `"6"`

#### Example 2

Input: `num1 = "123", num2 = "456"`

Output: `"56088"`

#### How to Solve

The problem requires no direct convert to integer, also, no BigInteger library. This means the solution considers that the numbers may be big enough to overflow while multiplying.

The solution here takes an approach as if the multiplication is done by hand.

```
     456
*)   123
 -------
    1368
    912
+) 456
 -------
   56088
```

The first part calculates `num2 * (one digit from num1)` and saves it in an array. Each array element is at most `9 * num2`. The second part is an addition. Not to make the sum bigger, two are processed at a time. After summing up the two, get division and modulo by 10. The remainder is added to the result as a string. The quotient is used to the next sum.

#### Solution

- Python

```python
class Multiply:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == '0' or num2 == '0': return '0'
        m, n = len(num1), len(num2)
        order1, memo = 1, []

        for i in range(m-1, -1, -1):
            carry, sub, order2 = 0, 0, 1
            d1 = ord(num1[i]) - ord('0')
            for j in range(n-1, -1, -1):
                d2 = ord(num2[j]) - ord('0')
                carry, rem = divmod(carry + d1 * d2, 10)
                sub += order2 * rem
                order2 *= 10
            sub += order2 * carry
            memo.append(sub)

        prev, d = divmod(memo[0], 10)
        result = str(d)
        for cur in memo[1:]:
            prev, d = divmod(prev + cur, 10)
            result = str(d) + result
        if prev > 0:
            result = str(prev) + result
        return result
```

#### Complexity

- Time: `O(m*n)` -- m, n are lengths of two strings
- Space: `O(m)`