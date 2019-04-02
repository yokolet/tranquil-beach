# Binary Tree Zigzag Level Order Traversal

#### Description

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

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
  [20,9],
  [15,7]
]
```

#### How to Solve

The solution here uses breadth first search (BSF). In each level,
direction changes: right to left, left to right. When the next level goes from right to left, add nodes from left to right at the end of queue. Then take node out from the end of the queue. When the next level goes from left to right, add nodes from right to left. Then take node from the beginning of the queue.

#### Solution
- Python

```python
class ZigzagTraversal:
    def zigzagLevelOrder(self, root: TreeNode) -> 'List[List[int]]':
        if not root: return []
        queue, result = [root], []
        lr = False
        while queue:
            tmp = []
            for _ in range(len(queue)):
                if lr:
                    node = queue.pop()
                    tmp.append(node.val)
                    if node.right: queue.insert(0, node.right)
                    if node.left: queue.insert(0, node.left)
                else:
                    node = queue.pop(0)
                    tmp.append(node.val)
                    if node.left: queue.append(node.left)
                    if node.right: queue.append(node.right)
            result.append(tmp)
            lr = not lr
        return result
```

- Ruby

```ruby
# @param {TreeNode} root
# @return {Integer[][]}
def zigzag_level_order(root)
  return [] if root.nil?
  queue, lr, result = [root], false, []
  while !queue.empty?
    tmp = []
    queue.size.times do
      if lr
        node = queue.pop
        tmp << node.val
        queue.unshift(node.right) if !node.right.nil?
        queue.unshift(node.left) if !node.left.nil?
      else
        node = queue.shift
        tmp << node.val
        queue << node.left if !node.left.nil?
        queue << node.right if !node.right.nil?
      end
    end
    result << tmp
    lr = !lr
  end
  result
end
```

#### Complexity
- Time: O(n)
- Space: O(m) -- m is number of nodes in a single level