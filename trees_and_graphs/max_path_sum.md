# Binary Tree Maximum Path Sum

#### Description

Given a non-empty binary tree, find the maximum path sum.

- Definition

    A path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

#### Example 1
Input:
```
       1
      / \
     2   3
```

Output: `6`

#### Example 2
Input:
```
   -10
   / \
  9  20
    /  \
   15   7
```

Output: `42`

#### How to Solve

Do prerder traversal and calculate the value, `node value + left substree value + right subtree value`, which is the sum at the current root. Compare the value with the max value so far.
When returning the value, considerable paths are: root + left subtree, root + right subtree, or 0 (doesn't take this subtree).
Retuen the max value of those three.

What needs to be care is, how to save max value so far. Python solution pass it as a method argument and returns it. Ruby solution uses an instance variable. 

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class MaxPathSum:
    def maxPathSum(self, root: TreeNode) -> int:
        def walk(root: TreeNode, max_sofar: int) -> (int, int): # max_sofar, val for upper stack
            if not root: return max_sofar, 0
            max_sofar, l_max = walk(root.left, max_sofar)
            max_sofar, r_max = walk(root.right, max_sofar)
            max_sofar = max(max_sofar, root.val + l_max + r_max)
            return max_sofar, max(root.val + max(l_max, r_max), 0)
        max_value, _ = walk(root, float('-inf'))
        return max_value
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
def max_path_sum(root)
  @max_value = -Float::INFINITY
    walk = -> (root) {
      return 0 if root.nil?
      l_max = walk.call(root.left)
      r_max = walk.call(root.right)
      @max_value = [@max_value, root.val + l_max + r_max].max
      return [root.val + [l_max, r_max].max, 0].max
    }
    walk.call(root)
    @max_value
end
```

#### Complaxity
- Time: O(n)
- Space: O(h) -- h is a height of the tree