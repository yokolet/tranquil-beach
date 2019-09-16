# Valid Number

#### Description

Given a string, validate the string can be interpreted as a decimal number.

#### Examples

- True

```
"0"
" 0.1 "
"2e10"
" -90e3   "
" 6e-1"
"53.5e93"
".1"
"3."
```

- False

```
"abc"
"1 a"
" 1e"
"e3"
" 99e2.5 "
" --6 "
"-+3"
"95a54e53"
```

#### How to Solve

This solution uses a regular expression to deterimine the given string is a valid number or not. There should exist various solutions. For example, in Python, only `float(s)` and exception handling perfectly works. However, in Ruby, `s.to_f` doesn't work for this problem. This is because Ruby cuts invalid characters automatically and returns a decimal number.

The regex pattern considers:

- spaces at beginning and end
- sign + -
- digits 0-9
- exponent - "e"
- decimal point - "."


#### Solution
- Python

```python
import re

class ValidNumber:
    class ValidNumber:
    def isNumber(self, s: str) -> bool:
        pat = re.compile(r'^\s*[+-]?(\d+(\.\d*)?|\.\d+)([Ee][+-]?\d+)?\s*$')
        return True if pat.match(s) else False
```

- Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_number(s)
  return true if /^\s*[+-]?(\d+(\.\d*)?|\.\d+)([Ee][+-]?\d+)?\s*$/.match(s)
  false
end
```

#### Complexity
- Time: `O(n)` -- for Deterministic Finite Automata complied regex
- Space: `O(2^m)` -- m is regular expression size
