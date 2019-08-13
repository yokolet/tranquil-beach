# Add Binary

#### Description

Given two binary strings, return their sum, which is also a binary string.

The input strings are both non-empty and contains only characters 1 or 0.

#### Example 1
Input: a = "11", b = "1"

Output: "100"

#### Example 2
Input: a = "1010", b = "1011"

Output: "10101"

#### How to Solve

Both Python and Ruby have a handy function which runs fast. The first Python solution and Ruby are using such function -- convert strings to integer, add two, then convert back to binary string.

The second Python solution takes algorithmic approach. It iterates two strings from the end to head until a longer string pointer comes to the beginning.
In each interation, add the carry and 0 or 1, find a quotient and remainder, append the remainder at the head of result as a string.
In the end, if still carry is there, add '1' at the head of the result.

#### Solution 1
- Python

```python
class AddBinary:
    def addBinary(self, a: str, b: str) -> str:
        return bin(int(a, 2) + int(b, 2))[2:]
```

- Ruby

```ruby
# @param {String} a
# @param {String} b
# @return {String}
def add_binary(a, b)
  sprintf("%b", a.to_i(2) + b.to_i(2))
end
```

### Solution 2

- Python

```python
class AddBinary:
    def addBinary(self, a: str, b: str) -> str:
        result = ''
        idx_a, idx_b = len(a) - 1, len(b) - 1
        carry = 0
        while idx_a >= 0 or idx_b >= 0:
            v_a = 1 if idx_a >= 0 and a[idx_a] == '1' else 0
            v_b = 1 if idx_b >= 0 and b[idx_b] == '1' else 0
            carry, rem = divmod(carry + v_a + v_b, 2)
            result = str(rem) + result
            idx_a -= 1
            idx_b -= 1
        if carry == 1:
            result = '1' + result
        return result
```

#### Complexity

- Solution 1
    - Time: `O(1)`
    - Space: `O(1)`

- Solution 2
    - Time: `O(n)` -- n is a longer length of given strings
    - Space: `O(1)`