# Convert Binary Search Tree to Sorted Doubly Linked List

#### Description

Given a binary search tree, convert it to a sorted circular doubly-linked list. The conversion must be done in-place.

#### Example
Input:

```
    4
   / \
  2   5
 / \
1   3
```

Output:

```
+-------------------+
|                   |
v ->   ->   ->   ->
1    2    3    4    5
  <-   <-   <-   <- ^
|                   |
+-------------------+
```

#### How to Solve

The recursive approach is a good one here. Like other binary tree problems, the first step is to go deeper to the leaf node.
When coming back to previous stack, it returns both left and right children. In total, four children will be returned -- left of left child (`ll`), right of left child (`lr`), left of right child (`rl`) and right of right child (`rr`).

The predecessor is the left subtree's right most child(`lr`).
The successor is the right subtree's left most child(`rl`).
So, `root.left = lr, root.right = rl` are processed.
To make bidirectional, this node is set to lr.right and rl.left. `if lr: lr.right = root, if rl: rl.left = root`.

When all recursive call is done and comes back to the top stack, it returns the left most and right most nodes of the tree. The problem asks a circular linked list. Lastly, the far right and far left nodes are connected.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BSTToList:
    def treeToDoublyList(self, root: TreeNode) -> TreeNode:
        def walk(root):
            if not root: return None, None
            if (not root.left) and (not root.right): return root, root

            ll, lr = walk(root.left)
            rl, rr = walk(root.right)

            root.left = lr
            root.right = rl
            if lr: lr.right = root
            if rl: rl.left = root

            left = ll if ll else root
            right = rr if rr else root
            return left, right

        left, right = walk(root)
        if left: left.left = right
        if right: right.right = left
        return left
```

#### Complexity
- Time: `O(n)`
- Space: `O(h)` -- h is a height of the tree
