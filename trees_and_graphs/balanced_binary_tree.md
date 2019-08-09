# Balanced Binary Tree

#### Description

Given a binary tree, check if it is a height-balanced.

Definition ([Wikipedia: Binary tree](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees))

    A balanced binary tree is a binary tree structure in which the left and right subtrees of every node differ in height by no more than 1.

#### Example 1

Input:

```
    3
   / \
  9  20
    /  \
   15   7
```

Output: `True`

#### Example 2

Input:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Output: `False`

#### How to Solve

As in the description, whether balanced or not is determined by a height. Do postorder traversal, and check left and right subtrees' heights. When coming back to upper level, return the height so far and comparison result.

#### Solution

- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BalancedBinaryTree:
    def isBalanced(self, root: TreeNode) -> bool:
        def walk(root: TreeNode) -> (int, bool):
            if not root: return 0, True
            l_h, l_ret = walk(root.left)
            r_h, r_ret = walk(root.right)
            if not l_ret or not r_ret or abs(l_h - r_h) > 1:
                return l_h, False
            return 1 + max(l_h, r_h), True
        _, ret = walk(root)
        return ret
```

#### Complexity

- Time: O(n) -- n is a number of tree nodes
- Space: O(h) -- h is a height of the tree