# Flatten Binary Tree to Linked List

#### Description

Given a binary tree, flatten it to a linked list in-place.

#### Example
Input:

```
    1
   / \
  2   5
 / \   \
3   4   6
```

Output:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

#### How to Solve

Recursively go down to the right bottom while passing current node as previous node. When it comes back from child nodes,
set previous to right child and None to left child.
When coming back from leaf to root nodes, the tree is flattened. 

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BinaryTreeToList:    
    def flatten(self, root: 'TreeNode') -> 'None':
        """
        Do not return anything, modify root in-place instead.
        """
        def walk(root, prev):
            if not root: return prev
            prev = walk(root.right, prev)
            prev = walk(root.left, prev)
            root.right = prev
            root.left = None
            return root
        walk(root, None)
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
# @return {Void} Do not return anything, modify root in-place instead.
def flatten(root)
  walk(root, nil)
end
def walk(root, prev)
  return prev if root.nil?
  prev = walk(root.right, prev)
  prev = walk(root.left, prev)
  root.right = prev
  root.left = nil
  root
end
```

#### Complexity
- Time: O(n)
- Space:  O(h) -- h is a height of a binary tree