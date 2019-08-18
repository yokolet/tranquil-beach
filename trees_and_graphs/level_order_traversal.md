# Binary Tree Level Order Traversal

#### Description

Given a binary tree, return the level order traversal of its nodes' values. The level order traversal means traversing left to right, level by level.

#### Example
Input:
```
    3
   / \
  9  20
    /  \
   15   7
```

Output:
```
[
  [3],
  [9,20],
  [15,7]
]
```

#### How to Solve

The solution takes BFS (breadth first search).
In each level, the node value is added to the array from left to right.
How to maintain queue is not the same in Python and Ruby code.
Python uses an additional array, while Ruby uses shift method (pop equivalent). In both cases, the maximum size of the queue is the tree's widest width.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class LevelOrderTraversal:
    def levelOrder(self, root: TreeNode) -> 'List[List[int]]':
        if not root: return []
        queue = [root]
        result = []
        while queue:
            result.append([])
            for _ in range(len(queue)):
                cur = queue.pop(0)
                result[-1].append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
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
# @return {Integer[][]}
def level_order(root)
  return [] if root.nil?
  queue = [root]
  result = []
  while !queue.empty?
    result << []
    queue.length.times do
      q = queue.shift
      result[-1] << q.val
      queue << q.left if q.left
      queue << q.right if q.right
    end
  end
  result
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(w)` -- w is width of a binary tree
