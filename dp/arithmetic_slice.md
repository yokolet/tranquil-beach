# Arithmetic Slice

#### Description

Given an array of intergers, find a number of arithmetic slices.

- Definition

    The arithmetic slice is an subarray whose value difference between the neighboring elements are the same. If `ary[i+1] == ary[i]` for all `i (0 <= i < length of ary - 1)` and the length of ary is more than or equal to 3, it is the arithmetic slice.

#### Exmaple

Input: `[1,2,3,4]`

Output: `3`

Explanation: `[1,2,3], [2,3,4], [1,2,3,4]` are arithmetic slices.

#### How to Solve

The problem asks how many patterns of arithmetic slices(subarrays) are there. The dynamic programming (DP) is a good approach. An auxiliary array is used to save the state so far. The array saves the number of patters at each index. Starting from the difference of index 1 and 0, update the number as long as the difference is the same. When it comes to another difference, re-start with the new difference from that index. At the end,
sum up all values in the auxiliary array which will be the answer.

#### Solution

- Python

```python
class ArithmeticSlice:
    def numberOfArithmeticSlices(self, A: 'List[int]') -> int:
        if len(A) < 3: return 0
        memo = [0 for _ in range(len(A))]
        diff = A[1] - A[0]
        for i in range(2, len(A)):
            if A[i] - A[i-1] == diff:
                memo[i] = memo[i-1]+1
            else:
                diff = A[i] - A[i-1]
        return sum(memo)
```

#### Complexity

- Time: O(n) -- n is a length of the array
- Space: O(n)