# Diameter of Binary Tree

#### Description

Given a binary tree, find the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of path between two nodes is represented by the number of edges between them.

#### Example
Input:

```
    1
   / \
  2   3
 / \     
4   5    
```

Output: 3

Explanation: A path [4, 2, 1, 3] or [5, 2, 1, 3] is the longest whose edges are 3.

#### How to Solve

The diameter is calculated from a height. A current diameter will be a sum of left and right heights. Compare, current, left and right diameters. The current deeper height will be the height of upper recursion stack.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BinaryTreeDiameter:
    def diameterOfBinaryTree(self, root: 'TreeNode') -> int:
        def walk(root: 'TreeNode') -> (int, int): # hegiht, diameter
            if not root: return 0, 0
            l_h, l_d = walk(root.left)
            r_h, r_d = walk(root.right)
            h = 1 + max(l_h, r_h)
            d = max(l_h + r_h, l_d, r_d)
            return h, d

        _, d = walk(root)
        return d
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
# @return {Integer}
def diameter_of_binary_tree(root)
  _, d = walk(root)
  d
end
def walk(root) # returns height and diameter
  return 0, 0 if root.nil?
  l_h, l_d = walk(root.left)
  r_h, r_d = walk(root.right)
  h = 1 + [l_h, r_h].max
  d = [l_h + r_h, l_d, r_d].max
  return h, d
end
```

#### Complexity
- Time: O(n)
- Space: O(h) -- h is a hight of a binary tree