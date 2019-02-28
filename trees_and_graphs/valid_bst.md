# Validate Binary Search Tree

#### Description

Given a binary tree, determine if it is a valid binary search tree (BST).

Definition of BST:
- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

#### Example 1
Input:

```
    2
   / \
  1   3
```

Output: True

#### Example 2
Input:
```
    5
   / \
  1   4
     / \
    3   6
```

Output: False

Explanation: The right child of root node has a smaller value than root value.

#### How to Solve

Give lower and upper bound and recursively go over all nodes.
When it goes left, upper bound will be a root node value. When it goes right, lower bound will be root node value.
If `lower < root.val < upper`, go deeper. If not, return false.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class ValidBST:
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def walk(root, lower, upper):
            if not root: return True
            if root.val > lower and root.val < upper:
                return walk(root.left, lower, root.val) and walk(root.right, root.val, upper)
            else:
                return False
        return walk(root, float('-inf'), float('inf'))
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
# @return {Boolean}
def is_valid_bst(root)
  walk(root, nil, nil)
end
def walk(root, lower, upper)
  return true if root.nil?
  if (lower.nil? || root.val > lower) &&
      (upper.nil? || root.val < upper)
    return walk(root.left, lower, root.val) &&
        walk(root.right, root.val, upper)
  else
    return false
  end
end
```

#### Complexity
- Time: O(n)
- Space: O(h) -- h is a height of BST