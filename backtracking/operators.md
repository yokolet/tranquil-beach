# Expression Add Operators

#### Description

Given a string that contains only digits 0-9 and a target value, return all possibilities to add binary operators (not unary) +, -, or * between the digits so they evaluate to the target value.

#### Example 1
Input: `num = "123"`, `target = 6`

Output: `["1+2+3", "1*2*3"] `

#### Example 2
Input: `num = "232"`, `target = 8`

Output: `["2*3+2", "2+3*2"]`

#### Example 3
Input: `num = "105"`, `target = 5`

Output: `["1*0+5","10-5"]`

#### Example 4
Input: `num = "00"`, `target = 0`

Output: `["0+0", "0-0", "0*0"]`

#### Example 6
Input: `num = "3456237490"`, `target = 9191`

Output: `[]`

#### How to Solve

Take a character from the string one by one, apply 3 operators to the single character, then repeat recursively. Additionally, the solution should include 2 or more digits patterns, for eaxmple, `10 - 5`.
So, the solution takes 4 paths to iterate to the end.

#### Solution
- Python

```python
class Operators:
    def addOperators(self, num, target):
        """
        :type num: str
        :type target: int
        :rtype: List[str]
        """
        if not num: return []

        def dfs(i, expr, acc, last, cur):
            if i == n-1:
                if acc + last + values[i] == target:
                    result.append(expr + '+' + num[i])
                if acc + last - values[i] == target:
                    result.append(expr + '-' + num[i])
                if acc + last * values[i] == target:
                    result.append(expr + '*' + num[i])
                if cur and acc + last // cur * (10 * cur + values[i]) == target:
                    result.append(expr + num[i])
            else:
                dfs(i + 1, expr + '+' + num[i], acc + last, values[i], values[i])
                dfs(i + 1, expr + '-' + num[i], acc + last, -values[i], values[i])
                dfs(i + 1, expr + '*' + num[i], acc, last * values[i], values[i])
                if cur:
                    dfs(i + 1, expr + num[i], acc, last // cur * (10 * cur + values[i]), 10 * cur + values[i])

        values = [int(x) for x in num]
        n = len(values)
        if n ==1 :
            if values[0] == target:
                return [num]
            return []
        result = []
        dfs(1, num[0], 0, values[0], values[0])
        return result
```

- Ruby

```ruby
# @param {String} num
# @param {Integer} target
# @return {String[]}
def add_operators(num, target)
  return [] if num.nil? || num.empty?
  values = num.split('').map(&:to_i)
  n = values.size
  if n == 1
    return [num] if values[0] == target
    return []
  end
  result = []
  dfs = ->(i, expr, acc, last, cur) {
    if i == n - 1
      if acc + last + values[i] == target
        result << expr + '+' + num[i]
      end
      if acc + last - values[i] == target
        result << expr + '-' + num[i]
      end
      if acc + last * values[i] == target
        result << expr + '*' + num[i]
      end
      if cur > 0 and acc + last / cur * (10 * cur + values[i]) == target
        result << expr + num[i]
      end
    else
      dfs.call(i + 1, expr + '+' + num[i], acc + last, values[i], values[i])
      dfs.call(i + 1, expr + '-' + num[i], acc + last, -values[i], values[i])
      dfs.call(i + 1, expr + '*' + num[i], acc, last * values[i], values[i])
      if cur > 0
        dfs.call(i + 1, expr + num[i], acc, last / cur * (10 * cur + values[i]), 10 * cur + values[i])
      end
    end
  }
  dfs.call(1, num[0], 0, values[0], values[0])
  result
end
```

#### Complexity
- Time: O(4^n)
- Space: O(n)