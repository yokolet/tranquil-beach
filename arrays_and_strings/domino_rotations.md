# Minimum Domino Rotations For Equal Row

#### Description

Given two arrays of intergers, `A` and `B`, which repressents rows of a dominoes' top and bottom halves, find the minimum number of swaps of `A[i]` and `B[i]` so that all `A` or all `B` values are the same. 

#### Example 1
Input: `A = [2,1,2,4,2,2], B = [5,2,6,2,3,2]`

Output: `2`

Explanation: The choice to have all same values is 2 or 5. If 2 is chosen,
2 swaps at indices 1 and 3 give all 2 in A.

#### Example 2
Input: `A = [3,5,1,2,3], B = [3,6,3,3,4]`

Output: `-1`

Explanation: The only one choice is 3, but it's unable to make it 3 at index 1.

#### How to Solve

At first, the solution finds the most used value in A and B. If the frequency is less than the length of A, it's unable to have the same value in all indices. If the valid most used value is found, go over the two arrays. If both `A[i]` and `B[i]` are not the most used value, the answer is -1. If `A[i]` is not, it should be swaped, so count up for `A`.
Do the same for `B`, then find the minimum swap counts.

#### Solution

- Python

```python
from collections import Counter

class DominoRotations:
    def minDominoRotations(self, A: 'List[int]', B: 'List[int]') -> int:
        n = len(A)
        count = Counter(A + B)
        if count.most_common(1)[0][1] < n:
            return -1
        v = count.most_common(1)[0][0]
        cnt_a, cnt_b = 0, 0
        for i in range(n):
            if A[i] != v and B[i] != v: return -1
            elif A[i] != v and B[i] == v:
                cnt_a += 1
            elif A[i] == v and B[i] != v:
                cnt_b += 1
        return min(cnt_a, cnt_b)
```

#### Conplexity
- Time: `O(n)` -- n is a length of `A` and `B`
- Space: `O(1)`