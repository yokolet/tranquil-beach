# Decode Ways

#### Description

Given a non-empty string containing only digits, determine the total number of ways to decode it.

The mapping from letters, A-Z, to digits is defined:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

#### Example 1
Input: `"12"`

Output: `2`

Explanation: "AB" (1 2) or "L" (12) are possible decode ways.

#### Example 2
Input: `"226"`

Output: `3`

Explanation: "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6) are possible decode ways.

#### How to Solve

The solution here takes a dynamic programming approach.
Previous states are saved in an auxiliary array.
The array saves how many patters eixts at the index i.

It starts from an empty state, `i = 0`, which has one decode way. When only the first digit is looked at, the decode way is one. Then, the loop starts. The ones and tens places are checked at each index i. When the loop is over, the answer is on the last element of the auxiliary array.


#### Solution
- Python

```python
class DecodeDigits:
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s or s[0] == '0': return 0
        n = len(s)
        memo = [0]*(n + 1)
        memo[0] = 1 # s is empty
        memo[1] = 1 # s[0] is 1 to 9
        for i in range(2, n+1):
            ones, tens = s[i - 1], s[i - 2]
            if ones >= '1' and ones <= '9':
                memo[i] += memo[i - 1]
            if tens == '1' or (tens == '2' and ones <= '6'):
                memo[i] += memo[i - 2]
        return memo[n]
```

- Ruby

```ruby
# @param {String} s
# @return {Integer}
def num_decodings(s)
  return 0 if s.empty? || s[0] == '0'
  n = s.size
  memo = Array.new(n + 1, 0)
  memo[0] = 1 # 0 length
  memo[1] = 1 # s[0] must be 1-9
  (2..n).each do |i|
    ones, tens = s[i - 1], s[i - 2]
    if ones >= '1' && ones <= '9'
      memo[i] += memo[i - 1]
    end
    if tens == '1' || (tens == '2' and ones <= '6')
      memo[i] += memo[i - 2]
    end
  end
  memo[n]
end
```

#### Complexity
- Time: O(n)
- Space: O(n)