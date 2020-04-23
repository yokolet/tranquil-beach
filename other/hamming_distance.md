# Hamming Distance

#### Description

Given two integers, `x` and `y`, calculate the Hamming distance. The definition of the Hamming distance is below. The range of two integers are `0 <= x, y < 2^31`.

- Definition of the Hamming distance
    - The number of positions at which the corresponding bits are different.

#### Example

Input: `x = 1, y = 4`

Output: `2`

Explanation:
```
1:    0 0 1
4:    1 0 0
      ^   ^
      two are different
```

#### How to Solve

After taking the XOR, the problem can be solved using [Brian Kernighan's Algorithm](http://graphics.stanford.edu/~seander/bithacks.html#CountBitsSetKernighan). The algorithm uses the trait of the binary number when 1 is subtracted by the original number, after and including the rightmost bit value 1 are flipped.

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

Repeat flipping the bits unless the number is greater than 0. The number of repetitions is the answer.

- Similar problem
    - [Bitwise AND of Numbers Range](bitwise_and.md)

#### Solution
- Python

```python
class HammingDistance:
    def hammingDistance(self, x: int, y: int) -> int:
        xor = x ^ y
        dist = 0
        while xor:
            dist += 1
            xor &= (xor - 1)
        return dist
```

#### Complexity
- Time: `O(1)` -- the given number of upper bound is fixed, so it is constant
- Space: `O(1)`
