# Minimum Swaps to Make Sequences Increasing

#### Description

Given two arrays of integers of the same none-zero length, find the minimum number of swaps to make both sequences strictly increasing.
By swapping, two arrays, `A` and `B` will be:
`A[0] < A[1] < A[2] < ... < A[A.length - 1]` and
`B[0] < B[1] < B[2] < ... < B[B.length - 1]` at the end.
It is guaranteed that the given arrays always makes it possible.

#### Example

Input: `A = [1,3,5,4], B = [1,2,3,7]`

Output: 1

Explanatin: swap `A[3]` and `B[3]`

#### How to solve

Maintain the state at each index `i` based on the previous state `i-1`.
The possible states are: the swap didn't happen at both `i-1` and `i`, happened at both `i-1` and `i`, only at `i-1`, or only at `i`.
To cover those 4 caes, look at the case, `max(A[i-1], B[i-1]) < min(A[i], B[i])` first. This means: either the swap happened or not at index `i-1`, the swap won't happen at index `i`. The no swaps state at index `i` should be the minimum of no swaps or swaps. Then, increment the swaps by one.
The second case is `A[i-1] < A[i] and B[i-1] < B[i]`. If the swap happened at index `i-1` and so should do at index `i`. In this case, update the swaps.
The third case is: if the swap did not happen at index `i-1`, it should happen at index `i`. Update the swap by incrementing no swaps by one.
In the end, minimum of swaps and no swaps gives the answer.

#### Solution
- Python

```python
class MinSwaps:
    def minSwap(self, A: 'List[int]', B: 'List[int]') -> int:
        x, y = 0, 1 # x: no swap, y: swap
        for i in range(1, len(A)):
            if max(A[i-1], B[i-1]) < min(A[i], B[i]):
                # swap at i-1 and no swap at i
                # no swap at i-1 and no swap at i
                x = y = min(x, y)
                y += 1
            elif A[i-1] < A[i] and B[i-1] < B[i]:
                # swap at i-1 and swap at i
                y += 1 
            else:
                # no swap at i-1 and swap at i
                x, y = y, x + 1
        return min(x, y)
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(1)`
