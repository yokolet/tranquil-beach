# Bitwise AND of Numbers Range

#### Description

Given two integers, `m` and `n`, which represent a range `[m,n]`, return the bitwise AND of all numbers in the range inclusive. The range is `0 <= m <= n 2147483647`.

#### Example 1

Input: `m=5,n=7`

Output: `4`

#### Example 2

Input: `m=0,n=1`

Output: `0`

#### How to Solve

The problem can be solved using [Brian Kernighan's Algorithm](http://graphics.stanford.edu/~seander/bithacks.html#CountBitsSetKernighan).
The algorithm uses the trait of the binary number when 1 is subtracted by the original number, after and including the rightmost bit value 1 are flipped.

```
10:    1010
         ^
         rightmost 1

 9:    1001
          ^
          rightmost 1

 8:    1000
       ^
       rightmost 1

 7:    0111
          ^
          rightmost 1

 6:    0110
 ...
```

Starting from a bigger number `n`, take bitwise AND with `n-1` while the number is bigger than the smaller value `m`. In the end, take bitwise AND with the `m`. That the answer.

- Similar problem:
    - [Hamming Distance](hamming_distance.md)

#### Solution
- Python

```python
class BitwiseAnd:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        while m < n:
            n &= (n - 1)
        return m & n
```

#### Complexity
- Time: `O(1)` -- the given number of upper bound is fixed, so it is constant
- Space: `O(1)`
