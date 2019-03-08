# Construct Binary Tree from Preorder and Inorder Traversal

#### Description

Given preorder and inorder traversal of a tree, construct the binary tree.

Duplicates do not exist in the tree.

#### Example
Input:

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Output:

```
    3
   / \
  9  20
    /  \
   15   7
```

#### How to Solve

The first element in preorder is a root, while the same value in inorder divides left and right subtree.

```
preorder = [|3|,9,20,15,7]
inorder = [9,|3|,15,20,7]
```

Recursively, repeat go left and right subtree by creating a root node, and adding left and right child from subtree.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class PreorderInorder:
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        def build(p_iter, p_start, p_end):
            if p_start > p_end: return None
            val = next(p_iter)
            node = TreeNode(val)
            node.left = build(p_iter, p_start, idx_dict[val] - 1)
            node.right = build(p_iter, idx_dict[val]+ 1, p_end)
            return node
        idx_dict = {v: i for i, v in enumerate(inorder)}
        return build(iter(preorder), 0, len(preorder)-1)
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

# @param {Integer[]} preorder
# @param {Integer[]} inorder
# @return {TreeNode}
def build_tree(preorder, inorder)
  return [] if inorder.empty?
  idx_h = inorder.zip(inorder.size.times).to_h
  build(preorder, 0, preorder.size - 1, idx_h)
end
def build(preorder, p_start, p_end, idx_h)
  return nil if p_start > p_end
  val = preorder.shift
  node = TreeNode.new(val)
  node.left = build(preorder, p_start, idx_h[val] - 1, idx_h)
  node.right = build(preorder, idx_h[val] + 1, p_end, idx_h)
  node
end
```

#### Complexity
- Time: O(n)
- Space: O(n)