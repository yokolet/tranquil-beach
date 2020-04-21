# Construct Binary Search Tree from Preorder Traversal

#### Description

Given a preorder traversal node value list, construct a binary search tree and return the root node.

#### Example

Input: `[8,5,1,7,10,12]`

Output:
```
      8
    /   \
   5     10
 /  \      \
1    7      12
```

#### How to Solve

The solution here takes a recursive approach.
This is a binary search tree, so the first value is a root node. The less values than the first value go to a left subtree and the rest of values go to a right subtree. This pattern is always the same when the input array is divided to left and right subtree values.
Find the index of the first value greater than the first one. That is the division point. Then apply the same logic to left and right subtrees.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BSTByPreorder:
    def bstFromPreorder(self, preorder: 'List[int]') -> TreeNode:
        def build(arr):
            if not arr: return None
            n = TreeNode(arr[0])
            if len(arr) == 1: return n
            idx = 1
            while idx < len(arr) and arr[idx] < arr[0]:
                idx += 1
            n.left = build(arr[1:idx])
            n.right = build(arr[idx:])
            return n
        return build(preorder)
```

#### Complexity
- Time: `O(nlog(n))` -- n is a length of the given array
- Space: `O(h)` -- h is a height of the tree
