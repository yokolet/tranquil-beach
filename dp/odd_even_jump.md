# Odd Even Jump

#### Description

Given an array of integers `A`, find how many indices are reachable to the last index with the jump definitions below:

- A jump goes from index `i` to index `j`.
- Jumps always go from left to right, `i < j`.
- All indices can be a starting index.
- The numbered jumps are starts from odd, then followed by even, odd, even, ...
- The odd numbered jump should go the index satisfies `A[i] <= A[j]`.
- The even numbered jump should go to the index satisfies `A[i] >= A[j]`.
- Multiple indices satisfy conditions above, the smallest index is the next position.
- The number of valid jumps will be 0 or more.

#### Example 1
Input: `[10,13,12,14,15]`

Output: `2`

Explanation: Successful jumps are index 3->4 and 4 (no jump).

When the start index is 0, the first jump is one of indices 1, 3, 4. The smallest is 1. The second jump is possible to only index 2. The third jump is one of indices 3, 4. The smallest is 3. The forth jump should go to less than or equal to 14, but no such value exists. So, the index 0 is not good.

#### Example 2
Input: `[2,3,1,1,4]`

Output: `3`

Explanation: Successful jumps are index 1->4, 3->4, and 4 (no jump).

#### Example 3
Input: `[5,1,3,4,2]`

Output: `3`

Explanation: Successful jumps are index 1->2->4, 2->3->4, and 4 (no jump).

#### How to Solve

This problem asks indices of non descreasing subsequence for the odd numbered jumps and non increasing subsequence for the even numbered jumps.
In the second example, `[2,3,1,1,4]`, if the start index is 0, non descreasing subsequence after index 0 is `[3, 4]`. The smallest index is 1 in the original array. This is the first jump. The second jump finds the non increasing subsequence after index 1. It is `[1, 1]`. The smallest index is 2 in the original array.  The third jump goes back to find non descreasing subsequence, which is `[1,4]`. The smallest index is 3 in the original array. The forth jump finds non increasing subsequence which doesn't exist.

One of approcahes for this type of problem is to use monotonic increaseing/descreasing stacks. The stack saves next jumping indices.
After creating the two monotonic stacks for odd and even jumps, iterate over the array from right to left. This is because the problem asks a number of Trues. Starting from the index `n-2`, check the indices are reachable to the last index. Since the jumps may or may not have multiple hops, use two auxiliary arrays to save the previous states.

In the end, the number of Trues in the odd jumps is the answer. The reason of the odd is the first jump is always the odd numbered. Apparenty, 1 is odd number.

#### Solution

- Python

```python
class OddEvenJump:
    def oddEvenJumps(self, A: 'List[int]') -> 'int':
        n = len(A)

        def makeNext(indices):
            result = [None for _ in range(len(indices))]
            stack = []
            for i in indices:
                while stack and i > stack[-1]:
                    result[stack.pop()] = i
                stack.append(i)
            return result

        a = [(v, i) for i, v in enumerate(A)]
        indices = [i for _, i in sorted(a, key=lambda x: x[0])]
        next_odd = makeNext(indices)
        indices = [i for _, i in sorted(a, key=lambda x: x[0], reverse=True)]
        next_even = makeNext(indices)

        odds, evens = [False for _ in range(n)], [False for _ in range(n)]
        odds[-1], evens[-1] = True, True

        for i in range(n-2, -1, -1):
            if next_odd[i] is not None:
                odds[i] = evens[next_odd[i]]
            if next_even[i] is not None:
                evens[i] = odds[next_even[i]]
        return sum(odds)
```

#### Complexity
- Time: `O(nlog(n))` -- n is a length of given array
- Space: `O(n)`