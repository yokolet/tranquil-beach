# Count and Say

#### Description

Given an integer `n (1 <= n <= 30)`, generate the n-th term of the count-and-say sequence and return it as a string.

- Definition

    The count-and-say sequence is the sequence of integers below:

    ````
    n-th  seq
    1     1
    2     11
    3     21
    4     1211
    5     111221
    ````

    1. `"1"` - one 1 -> 11
    2. `"11"` - two 1 -> 21
    3. `"1211"` - one 2 one 1 -> 1211
    4. `"111221"` - one 1 one 2 two 1

#### Example 1

Input: `1`

Output: `"1"`

#### Example 2

Input: `4`

Output: `"1211"`

#### How to Solve

All count-and-say sequence numbers up to n-th need to be generated one by one. To create n-th sequence, check each digit of the (n-1)-th sequence from left to right. Count the same digits. When another digit is found, update the result string with the count and digit. At the end of the single sequence loop, update the result string with the count and digit.

#### Solution

- Python

```python
class Compression:
    def countAndSay(self, n: int) -> str:
        if n == 1: return '1'
        cur, prev = '', '1'
        for _ in range(n-1):
            count, p = 0, prev[0]
            for i in range(len(prev)):
                if prev[i] == p:
                    count += 1
                else:
                    cur += str(count) + p
                    count, p = 1, prev[i]
            cur += str(count) + p
            cur, prev = '', cur
        return prev
```

#### Complexity

- Time: `O(n^2)`
- Space: `O(1)`