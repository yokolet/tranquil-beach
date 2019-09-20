# Binary Tree Coloring Game

#### Description

Given a binary tree, number of nodes and the node value chosen by the first player, find whether the second player wins or not.

- Definition:
    - `n` is odd
    - Node values are distinct from `1` to `n`.
    - The first player's choice is `1 <= x <= n`.
    - The second player chooses one from `1 <= y <= n, y != x`.
    - Two players take turns starting from the first player.
    - In each turn, the player chooses a node from parent, left child or right child if those are not colored yet.
    - The player colors the node by its color.
    - The player can pass the turn only if it is unable to choose any.

#### Example
Input:

```
root
               1
          /        \
       2             [3]
    /    \          /  \
  4        5       6    7
/  \     /   \
8   9   10   11

n = 11, x = 3
```

Output: `true`

Explanation: The second player can choose node 1

#### How to Solve

For the frist step, the node of value x should be found.
Then, count the number of nodes in the left and right subtree of x.
The total number of nodes, `n`, is given. So, if the second player chooses the parent of x, possible counts are `n - (1 + left subtree + right subtree)`.
The second player can choose the starting node from:
- x's parent
- x's left child
- x's right child

If the maximum number of nodes among three exceeds `n/2`, the second player wins.


#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BinaryTreeColoring:
    def btreeGameWinningMove(self, root: TreeNode, n: int, x: int) -> bool:
        def findX(root, x):
            if not root: return None
            if root.val == x: return root
            left = findX(root.left, x)
            right = findX(root.right, x)
            return left or right

        def count(root):
            if not root: return 0
            return 1+count(root.left)+count(root.right)

        node_x = findX(root, x)
        left = count(node_x.left)
        right = count(node_x.right)
        return max(n - (1 + left + right), left, right) > n // 2
```

#### Complexity
- Time: `O(n)` -- n is a number of nodes
- Space: `O(h)` -- h is a height of the tree