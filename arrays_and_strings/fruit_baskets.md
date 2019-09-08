# Fruit Into Baskets

#### Description

Given an array of integers, `tree`, where each element represents a type of fruit,
find the maximum amount of two types of fruits available to be collected.

To collect the fruit, rules below are applied:

1. Always pick a piece of fruit from current tree if the collected types will be less than or equal to 2. Otherwise stop.
2. Always move one to the right until the end of the tree array.
3. A starting tree can be any.

#### Example 1

Input: `[1,2,1]`

Output: `3`

Explanation: Two types of fruits are collected from `[1,2,1]`

#### Example 2

Input: `[0,1,2,2]`

Output: `3`

Explanation: Two types of fruits are collected from `[1,2,2]`

#### Example 3

Input: `[1,2,3,2,2]`

Output: `4`

Explanation: Two types of fruits are collected from `[2,3,2,2]`

#### Example 4

Input: `[3,3,3,1,2,1,1,2,3,3,4]`

Output: `5`

Explanation: Two types of fruits are collected from `[1,2,1,1,2]`

#### How to Solve

Two pointers will be used to solve this problem. The left pointer keeps the leftmost occurence of one of two types.
The right pointer always goes right one by one.
To save the last occurence of each fruit type, a dictionary, `memo` is used. When the size of `memo` exceeds two, the solution finds the minimum index in the `memo` and delete the fruit type. This way, the deleted fruit type won't be recounted. Lastly, compare the `max_length` so far and `i-left+1`.

Similar problem: [Longest Substring With At Most K Distinct Characters](longest_substring_k_distinct.md)

#### Solution

- Python

```python
class FruitBaskets:
    def totalFruit(self, tree: 'List[int]') -> int:
        left, max_len, memo = 0, 0, {}
        for i in range(len(tree)):
            memo[tree[i]] = i
            if len(memo) > 2:
                left = min(memo.values())
                del memo[tree[left]]
                left += 1
            max_len = max(max_len, i-left+1)
        return max_len
```

#### Complexity

- Time: `O(n)` -- n is a length of the given array
- Space: `O(n)`
