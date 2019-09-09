# Count Complete Tree Nodes

#### Description

Given a complete binary tree, find how many node are in the tree.

- Definition of a complete binary tree

    In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.
    (Wikipedia: [Types of Binary Tree](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees))

#### Example

Input:

```
    1
   / \
  2   3
 / \  /
4  5 6
```

Output: `6`

#### How to Solve

A naive approach is to traverse all nodes and count. However, easy to imagine, it runs very slow.
The problem here is asking efficient way of counting by a property of the complete binary tree.

The complete tree problems often imply a comparison of left and right subtree heights (or depths). When calculating the height, aside from the starting node, always it goes left. This comes from the porperty of the complete binary tree whose node is left packed. When left and right subtree's heights are the same, the level of that subtree are all filled.
So, adds the 2^(left (or right) height) as the node count of that level. Then, goes deeper to the right since the right subtree is filled. If not (left subtree is higher), adds the 2^(right height). Then, goes deeper to the left since the right subtree is not filled.

#### Solution

- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class CompleteTreeCount:
    def countNodes(self, root: TreeNode) -> int:
        if not root: return 0

        def height(root):
            if not root: return 0
            return 1 + height(root.left)
        
        l_h = height(root.left)
        r_h = height(root.right)
        if l_h == r_h:
            return 2 ** l_h + self.countNodes(root.right)
        else:
            return 2 ** r_h + self.countNodes(root.left)
```

#### Complexity

- Time: `O(log(n))`  -- n is a number of nodes in the tree
- Space: `O(h)` -- h is a height of the tree