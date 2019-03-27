# Excel Sheet Column Number

#### Description

Given a column title as appear in an Excel sheet, return its corresponding column number.

Numbers are below:

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```

#### Example 1
Input: `"A"`

Output: `1`

#### Example 2
Input: `"AB"`

Output: `28`

#### Example 3
Input: `"ZY"`

Output: `701`

#### How to Solve

Traverse the string from left to right. Convert the character to integer from 1 to 26. When it goes to a next charater, result's place should be increased. This is 26 based (instead of base 10) number, so `result *= 26` first and add up current character's integer counterpart. 

#### Solution
- Python

```python
class ColumnNumber:
    def titleToNumber(self, s: str) -> int:
        result = 0
        for c in s:
            result *= 26
            result += ord(c) - ord('A') + 1
        return result
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def title_to_number(s)
  result = 0
  s.size.times do |i|
    result *= 26
    result += (s[i].ord - 'A'.ord + 1)
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(1)