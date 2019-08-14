# Perfect Number

#### Description

Given an integer num, write a function to return True when it is a perfect number. Otherwise, return False.

- Definition

    The Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

#### Example
Input: `28`

Output: `True`

Explanation: `28 = 1 + 2 + 4 + 7 + 14`

#### How to Solve

Iterating from 2 to num while checking whether it is a divisor or not will give the answer. However, it runs very slow, so this problem's point is how to cut down the iteration.

Like finding prime number, sqrt(num) can be upper bound. For example, when 2 is a divisor, 28 / 2 = 14 is also a divisor. Given that, limit the iteration up to sqrt(num) and add up two numbers. In the end, if the sum is the same as num, the answer is true, otherwise false.  

#### Solution
- Python

```python
from math import ceil, sqrt

class PerfectNumber:
    def checkPerfectNumber(self, num: int) -> bool:
        if num <= 1: return False
        sum = 1
        for i in range(2, ceil(sqrt(num))):
            if num % i == 0:
                sum += i
                sum += num // i
        return sum == num
```

- Ruby

```ruby
# @param {Integer} num
# @return {Boolean}
def check_perfect_number(num)
  return false if num <= 1
  sum = 1
  upper_bound = Math.sqrt(num).ceil
  (2...upper_bound).each do |i|
    if num % i == 0
      sum += i
      sum += (num / i)
    end
  end
  sum == num
end
```

#### Complexity
- Time: `O(sqrt(n))`
- Space: `O(1)`