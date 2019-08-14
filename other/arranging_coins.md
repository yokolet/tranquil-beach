# Arranging Coins

#### Description

Arrange a total of n coins to form a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

#### Example 1
Input: 5

Output: 2

Explanation:

The coins can form the following rows:
```
¤
¤ ¤
¤ ¤
```

Because the 3rd row is incomplete, the answer is 2.

#### Example 2
Input: 8

Output: 3

Explanation:

The coins can form the following rows:
```
¤
¤ ¤
¤ ¤ ¤
¤ ¤
```

Because the 4th row is incomplete, the answer is 3.

#### How to Solve

This is a math problem. The number of each rows are:
```
1, 2, 3, 4, ...
```

Accumulated sums are:
```
1, 3, 6, 10, ...
```

The nth accumulated sum is calculated by `n * (n + 1) / 2`.
The answer is to find `n` whose accumulated sum is less than or equal to a given number.

Let n be given number of coins and replace n to x in above formula, x can be found as in below.

```
x * (x + 1) / 2 <= n
x^2 + x <= 2n
x^2 + x - 2n <= 0
# quadratic formula to solve ax^2 + bx + c = 0 is:
# x = (-b + sqrt(b^2 - 4 * a * c)) / 2 * a
# x = (-b - sqrt(b^2 - 4 * a * c)) / 2 * a
# the first one is the formula to solve this problem
# plugin a = 1, b = 1 and c = -2n to the formula
x = (-1 + sqrt(1 + 8n)) / 2
# the answer should be floor of x
answer = floor(x)
```

In Python code, `int(x)` is faster than `math.floor(x)`, so `int` is used in the solution. In Ruby, `to_i` and `floor` runs in the same speed.

#### Solution
- Python

```python
import math

class Coins:
    def arrangeCoins(self, n: 'int') -> 'int':
        return int((-1 + math.sqrt(1 + 8 * n))/2)
```

- Ruby

```ruby
# @param {Integer} n
# @return {Integer}
def arrange_coins(n)
  ((-1 + Math.sqrt(1 + 8 * n)) / 2).to_i
end
```

#### Complexity
- Time: `O(1)`
- Space: `O(1)`