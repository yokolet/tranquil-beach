# Smallest Subtree with All the Deepest Nodes

#### Description

Given a binary tree, find the smallest subtree which has the deepest nodes. The values in the tree are all unique.

-  Definition

    deepest: the biggest depth in the entire tree

#### Example

Input:

```
        3
     /     \
   5         1
 /  \      /  \
6    2    0    8
    /  \
   7    4
```

Output:

```
   2
 /  \
7    4 
```

#### How to Solve

Recursively traversing the tree (DFS) is one of the approach. When going down to leaf nodes, increment the depth by one. When coming back from the leaf nodes, return a node and depth. After both left and right subtree are traversed, check what node and depth should be returned. If the depths from left and right are the same, the root node will be returned with the left or right depth. Otherwise, the deeper depth's node and depth are returned.

#### Solution

- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class DeepestSmallestSubtree:
    def subtreeWithAllDeepest(self, root: TreeNode) -> TreeNode:
        def walk(root: TreeNode, depth: int) -> (TreeNode, int): # parent_node, depth
            if not root: return None, depth
            l_n, l_d = walk(root.left, depth+1)
            r_n, r_d = walk(root.right, depth+1)
            if l_d > r_d:
                return l_n, l_d
            elif r_d > l_d:
                return r_n, r_d
            else:
                return root, l_d
        node, _ = walk(root, 0)
        return node
```

#### Complexity

- Time: O(n) -- n is a number of tree nodes
- Space: O(h) -- h is a height of the tree