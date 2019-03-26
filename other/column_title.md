# Excel Sheet Column Title

#### Description

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

Titles are below:

```
1 -> A
2 -> B
3 -> C
...
26 -> Z
27 -> AA
28 -> AB 
...
```

#### Example 1
Input: `1`

Output: `"A"`

#### Example 2
Input: `28`

Output: `"AB"`

#### Example 3
Input: `701`

Output: `"ZY"`

#### How to Solve

Each character can be expressed by base 26 without 0. Given that, subtract 1, then take modulo to find a character. The next iteration will be for the number n / 26.

#### Solution
- Python

```python
class ColumnTitle:
    def convertToTitle(self, n: int) -> str:
        result = ""
        while n:
            n -= 1
            result = chr((n % 26) + ord('A')) + result
            n //= 26
        return result
```

- Ruby

```ruby
# @param {Integer} n
# @return {String}
def convert_to_title(n)
  result = ""
  while n > 0
    n -= 1
    result = ((n % 26) + 'A'.ord).chr + result
    n /= 26
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(1)