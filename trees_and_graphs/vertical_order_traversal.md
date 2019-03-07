# Binary Tree Vertical Order Traversal

#### Description

Given a binary tree, return the vertical order traversal of its nodes' values. The vertical order traversal means to traverse from top to bottom, column by column.

If two nodes are in the same row and column, the order should be from left to right.

#### Example 1
Input:
```
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7 
```

Output:
```
[
  [9],
  [3,15],
  [20],
  [7]
]
```

#### Example 2
Input:
```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7 
```

Output:
```
[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```

#### Example 3
Input:
```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

0's right child is 2 and 1's left child is 5
```

Output:
```
[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

#### How to Solve

The solution uses BFS (breadth first search). While traversing, it adds a pair of node and left(negative) or right(positive) level to the queue. The node values are saved in a dictionary whoose key is left or right level. When the traversal is over, sort the dictionary by the key and return the values.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

from collections import defaultdict

class VerticalOrderTraversal:
    def verticalOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return []
        queue = [(root, 0)] # node, left(negative) or right(positive)
        result = defaultdict(list)
        while queue:
            node, lr = queue.pop(0)
            result[lr].append(node.val)
            if node.left:
                queue.append((node.left, lr - 1))
            if node.right:
                queue.append((node.right, lr + 1))
        return [result[k] for k in sorted(result.keys())]
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
def vertical_order(root)
  return [] if root.nil?
  result = {}
  queue = [[root, 0]] # [node, lr]
  while !queue.empty?
    node, lr = queue.shift
    result[lr] ||= []
    result[lr] << node.val
    if node.left
      queue << [node.left, lr - 1]
    end
    if node.right
      queue << [node.right, lr + 1
    end
  end
  result.sort.map(&:last)
end
```

#### Complexity
- Time: O(n) or O(vlog(v)) - n is a number of the node, v is a number of vertical orders.
- Space: O(n)