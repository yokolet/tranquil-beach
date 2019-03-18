# Roman to Integer

#### Description

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

- Definition

    Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

    ```
    Symbol       Value
    I             1
    V             5
    X             10
    L             50
    C             100
    D             500
    M             1000
    ```

    Roman numerals are usually written largest to smallest from left to right. However, exceptions are there. The one unit before 5, 10, 50, 100, 500, 1000 are expressed by 5-1, 10-1, 50-10, 100-10, 500-100, 1000-100. Those are IV(4), IX(9), XL(40), XC(90), CD(400), CM(900).

#### Example 1
Input: `"III"`

Output: `3`

#### Example 2
Input: `"IV"`

Output: `4`

#### Example 3
Input: `"IX"`

Output: `9`

#### Example 4
Input: `"LVIII"`

Output: `58`

#### Example 5
Input: `"MCMXCIV"`

Output: `1994`

Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

#### How to Solve

Traverse given string from left to right while adding the integer value to the result. Save previous letter and compare whether previous is samller than current letter or not. When previous is smaller, subtract 2*previous since previous values was added instead of subtracted.

#### Solution
- Python

```python
class RomanToInteger:
    def romanToInt(self, s: str) -> int:
        if not s: return 0
        table = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        result, prev = table[s[0]], table[s[0]]
        for c in s[1:]:
            cur = table[c]
            result += cur
            if cur > prev:
                result -= 2*prev
            prev = cur
        return result
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def roman_to_int(s)
  table = {'I'=>1, 'V'=>5, 'X'=>10, 'L'=>50, 'C'=>100, 'D'=>500, 'M'=>1000}
  result, prev = table[s[0]], table[s[0]]
  (1...s.size).each do |i|
    result += table[s[i]]
    if table[s[i]] > prev
      result -= 2*prev
    end
    prev = table[s[i]]
  end
  result
end
```

#### Complexity
- Time: O(1) -- the longest string is MMMCMXCIX
- Space: O(1)