# Validate Stack Sequences

#### Description

Given two sequences of distinct values, `pushed` and `popped`, return `True` if and only if the two sequences are the result of push and pop operations on an initially empty stack.

The popped array is a permutation of the pushed array.

#### Example 1

Input: `pushed = [1,2,3,4,5], popped = [4,5,3,2,1]`

Output: `True`

#### Example 2

Input: `pushed = [1,2,3,4,5], popped = [4,3,5,1,2]`

Output: `False`

#### How to Solve

Simulating push and pop operations will give the answer. The push operation is performed one by one, while the pop operation may repeat multiple times. Check the last value in the stack. As long as the last value in the stack is the same as the current value in the popped array, repeat popping from the stack and incrementing the index to the popped array. In the end, if stack is empty, the result is `True`.

#### Solution
- Python

```python
class StackSequences:
    def validateStackSequences(self, pushed: 'List[int]', popped: 'List[int]') -> bool:
        p, stack = 0, []
        for i in range(len(pushed)):
            stack.append(pushed[i])
            while p < len(popped) and len(stack) > 0 and stack[-1] == popped[p]:
                stack.pop()
                p += 1
        return len(stack) == 0
```

#### Complexity
- Time: `O(n)` -- n is a length of pushed (or popped) array
- Space: `O(n)`
