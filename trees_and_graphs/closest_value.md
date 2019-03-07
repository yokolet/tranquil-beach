# Closest Binary Search Tree Value

#### Description

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Given target value is a floating point.
Only one unique value in the BST that is closest to the target.

#### Example
Input:

```
    4
   / \
  2   5
 / \
1   3
```

Output: `4`

#### How to Solve

The solution takes a recursive approach. While comparing a closest value so far to a diff of current node value and target, go over the tree. If the target is greater than current node value, go right.
If the target is smaller than current node value, go left.  

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class ClosestValue:
    def closestValue(self, root: 'TreeNode', target: 'float') -> 'int':
        result = root.val
        if target < root.val and root.left is not None:
            result = self.closestValue(root.left, target)
        elif target > root.val and root.right is not None:
            result = self.closestValue(root.right, target)

        if abs(result - target) < abs(root.val - target):
            return result

        return root.val
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
# @param {Float} target
# @return {Integer}
def closest_value(root, target)
  result = root.val
  if root.val < target and root.right
    result = closest_value(root.right, target)
  end
  if root.val > target and root.left
    result = closest_value(root.left, target)
  end
  if (result - target).abs < (root.val - target).abs
    result
  else
    root.val
  end
end
```

#### Complexity
- Time: O(n)  -- n is a number of nodes in the tree
- Space: O(h) -- h is a height of the tree