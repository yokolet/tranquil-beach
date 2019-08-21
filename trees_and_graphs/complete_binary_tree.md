# Complate Binary Tree

#### Description

Given a binary tree, check if it is a complete binary tree.

- Definition ([Wikipedia: Binary tree](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees))

    In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes at the last level h.

#### Example 1

Input:

```
    1
   / \
  2   3
 / \  /
4   5 6
```

Output: `True`

#### Example 2

Input:

```
    1
   / \
  2   3
 / \   \
4   5   7
```

Output: `False`

#### How to Solve

Whether complete or not is determined by min and max heights at each node. If the right subtree has a bigger height, the tree is not complete. If the right subtree height is less than the left more than one, the tree is not complete. When the left min and max are not the same, the right min/max should be the same as left min. Do postorder traversal, and check left and right subtrees' heights. When coming back to upper level, return the min/max heights so far and comparison result.

#### Solution

- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class CompleteBinaryTree:
    def isCompleteTree(self, root: TreeNode) -> bool:
        def walk(root):
            if not root: return 0, 0, True
            l_min, l_max, l_ret = walk(root.left)
            r_min, r_max, r_ret = walk(root.right)
            ret = l_ret and r_ret
            if r_max > l_max:
                ret = False
            elif r_max+1 < l_max:
                ret = False
            elif l_min != l_max and (r_min != r_max or r_max != l_min):
                ret = False
            return 1+min(l_min, r_min), 1+max(l_max, r_max), ret
        _, _, ret = walk(root)
        return ret
```

#### Complexity

- Time: `O(n)` -- n is a number of nodes
- Space: `O(h)` -- n is a height of a tree
