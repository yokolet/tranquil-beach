# Longest Arithmetic Subsequence

#### Description

Given an array of intergers, return the longest length of an arithmetic subsequence.

- Definition

    The arithmetic sequence is the value difference between the neighboring elements are the same. If `ary[i+1] == ary[i]` for all `i (0 <= i < length of ary - 1)`, it is the arithmetic sequence.

#### Example 1

Input: `[3,6,9,12]`

Output: `4`

Explanation: The whole array is the arithmetic sequence.

#### Example 2

Input: `[9,4,7,2,10]`

Output: `3`

Explanation: `[4,7,10]` is the longest arithmetic subsequence.

#### EXample 3

Input: `[20,1,15,3,10,5,8]`

Output: `4`

Explanation: `[20,15,10,5]` is the longest arithmetic subsequence.

#### How to Solve

Since the problem asks a subsequence, the dynamic programming (DP) is the approach. In this case, an array of dictionaries is a good data structure to save a state so far. In each index of the auxiliary array, the key of the dictionary is a difference between index i and indices before i. The value is a length. While going over each index, update the maximum length.

#### Solution

- Python

```python
class ArithmeticSequence:
    def longestArithSeqLength(self, A: 'List[int]') -> int:
        memo = [{} for _ in range(len(A))]
        max_len = 0
        for i in range(1, len(A)):
            for j in range(i):
                diff = A[i] - A[j]
                if diff not in memo[j]:
                    memo[i][diff] = 2
                else:
                    memo[i][diff] = 1 + memo[j][diff]
                max_len = max(max_len, memo[i][diff])
        return max_len
```

#### Complexity

- Time: O(n^2) -- n is the length of the given array
- Space: O(n^2)