# Binary Tree Paths

#### Description

Given a binary tree, return all root-to-leaf paths.

A leaf is a node with no children.

#### Example

Input:

```
       1
     /   \
    2     3
     \
      5
```

Output: `["1->2->5", "1->3"]`


#### How to Solve

This is a pre-order traversal problem.
The traversal itself is not specific.
How to keep the values consistent should be considered carefully.
The traversal is done by a recursive call.
When it comes back from the call,
values of method arguments goes back to ones in previous stack.
In this solution, an array is used to hold all the paths to leaf nodes. The value of path should be back to previous one,
it is always passed as the method argument.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class TreePath:
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        def walk(root, path, result):
            path += str(root.val)
            if not root.left and not root.right:
                result.append(path)
            if root.left:
                walk(root.left, path+'->', result)
            if root.right:
                walk(root.right, path+'->', result)
        result = []
        if not root: return result
        walk(root, '', result)
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

# @param {String} s
# @return {TreeNode}
def binary_tree_paths(root)
    result = []
    return result if root.nil?
    walk(root, '', result)
    result
end

def walk(root, path, result)
    path += root.val.to_s
    result << path if root.left.nil? && root.right.nil?
    walk(root.left, path + '->', result) if root.left
    walk(root.right, path + '->', result) if root.right
end
```

#### Complexity
- Time: O(n)
- Space: O(h*l) -- h is a height of the tree, l is a number of leaf nodes
