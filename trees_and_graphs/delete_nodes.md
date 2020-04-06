# Delete Nodes and Return Forests

#### Description

Given the distinct value binary tree and values of nodes to be deleted, return a forest (a disjoint union of trees) after deleting all given nodes. The result is a list of the root of remaining forest. The list can be any order.

#### Example
Input: `root=[1,2,3,4,5,6,7]`, `to_delete=[3,5]`
```
      1
    /   \
  2      3
 / \    / \
4   5  6   7
```
Output: `[[1,2,null,4],[6],[7]]`

#### How to Solve

The solution here took the level order traversal using a queue. While traversing the tree from the top to bottom,
it checks the left and right children are in the delete list. If it is, set `None` as the left and/or right child values. Then, it checks the current node is on the delete list. If it is, the left and/or right children are added to the roots list if those exist. 

The recursive binary tree traversal also works.

#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class DeleteNodes:
    def delNodes(self, root: TreeNode, to_delete: 'List[int]') -> 'List[TreeNode]':
        target = set(to_delete)
        roots = []
        if root.val not in target: roots.append(root)
        queue = [root]
        while queue:
            cur = queue.pop(0)
            if cur.left:
                queue.append(cur.left)
                if cur.left.val in target: cur.left = None
            if cur.right:
                queue.append(cur.right)
                if cur.right.val in target: cur.right = None
            if cur.val in target:
                if cur.left: roots.append(cur.left)
                if cur.right: roots.append(cur.right)
        return roots
```

#### Complexity
- Time: `O(n)` -- n is a number of tree nodes
- Space: `O(w)` -- w is a width of binary tree
