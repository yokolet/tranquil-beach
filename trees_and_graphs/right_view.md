# Binary Tree Right Side View

#### Description

Given a binary tree, return an array of node values on the right most nodes in each level.

This is called a right side view which is to look at the tree from the right side.

#### Example
Input:

```
   1
 /   \
2     3
 \     \
  5     4
```

Output: `[1, 3, 4]`

#### How to Solve

Traverse the tree in order of right, then left. Keep the level while traversing the tree. If a deeper depth is found, add the node value to the result.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class RightView:
    def rightSideView(self, root: TreeNode) -> 'List[int]':
        depth, result = -1, []
        if not root: return result
        queue = [(root, 0)]
        while queue:
            node, level = queue.pop(0)
            if depth < level:
                result.append(node.val)
                depth = level
            if node.right:
                queue.append((node.right, level + 1))
            if node.left:
                queue.append((node.left, level + 1))
        return result
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
# @return {Integer[]}
def right_side_view(root)
  depth, result = -1, []
  return result if root.nil?
  queue = [[root, 0]]
  while !queue.empty?
    node, level = queue.shift
    if depth < level
      result << node.val
      depth = level
    end
    if node.right
      queue << [node.right, level + 1]
    end
    if node.left
      queue << [node.left, level + 1]
    end
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(h) -- h is a height of the tree