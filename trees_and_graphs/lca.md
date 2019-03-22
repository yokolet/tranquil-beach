# Lowest Common Ancestor of a Binary Tree

#### Description

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

- Definition

    The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants. A node may be a descendant of itself.

All of the nodes' values will be unique.
p and q are different and both values will exist in the binary tree.

#### Example 1
Input: `p = 5, q = 1`

```
         3
      /     \
     /       \
    5         1
  /   \     /   \
 6     2   0     8
     /   \
    7     4
```

Output: `3`

#### Example 2
Input: `p = 5, q = 4`

```
         3
      /     \
     /       \
    5         1
  /   \     /   \
 6     2   0     8
     /   \
    7     4
```

Output: `5`

#### How to Solve

Traverse the tree recursively in a postorder way. When a current root node is None (nil), p or q, return root. While coming back to upper stack, return value will be None (nil) or node of p or q. If both left and right are node, this current root is the loweset common ancestor.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Lca:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root or root == p or root == q: return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right: return root
        if left:
            return left
        else:
            return right
```

- Ruby

```ruby
class TreeNode
  attr_accessor :val, :left, :right

  def initialize(val)
    @val = val
    @left, @right = nil, nil
  end
end

# @param {TreeNode} root
# @param {TreeNode} p
# @param {TreeNode} q
# @return {TreeNode}
def lowest_common_ancestor(root, p, q)
  return root if !root || root == p || root == q
  left = lowest_common_ancestor(root.left, p, q)
  right = lowest_common_ancestor(root.right, p, q)
  return root if left && right
  left ? left : right
end
```

#### Complexity
- Time: O(n)
- Space: O(h) -- h is height of a tree