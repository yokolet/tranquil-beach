# Complete Binary Tree Inserter

#### Description

Write a data structure `CBTInserter` that is inialized with a complete binary tree and provides operations below:

- Operations

    - `CBTInserter(TreeNode root)`: initializes the data structure with the root of the complete binary tree
    - `insert(int v)`: inserts a new node with the value `v` to the tree and returns the value of the parent node. After the insertion, the tree should keep the completeness.
    - `get_root()`: returns the root node of the tree.


- Definition of a complete binary tree

    In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2^h nodes inclusive at the last level h.
    (Wikipedia: [Types of Binary Tree](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees))

#### Example 1

Iniital Tree:

```
1
```

```
obj = CBTInserter(root)
obj.insert(2) # => returns 1
obj.get_root()
```

Output:
```
   1
  /
2
```

#### Example 2

Iniital Tree:

```
    1
   /  \
  2    3
 / \   /
4   5 6
```

```
obj = CBTInserter(root)
obj.insert(7) # => returns 3
obj.insert(8) # => returns 4
obj.get_root()
```

Output:
```
      1
     /  \
    2    3
   / \   / \
  4   5 6   7
 /
8
```

#### How to Solve

The completeness of the binary tree is one of proerties that binary heaps have. The heap uses array to save a tree strucutre. The i-th element's left and right children are on the indices of `2*i+1` and `2*i+2`. The parent node of the i-th element is on the index `(i-1) / 2`.

Given that, the solution saves the nodes in the array like the binary heap. When a new node is inserted, it finds the parent node by calculating the index, and appends it as left or right child. Also, the new node is added to the array.

#### Solution

- Python

```python
class CBTInserter:
    def __init__(self, root: TreeNode):
        self.root = root
        self.memo = []
        queue = [root]
        while queue:
            cur = queue.pop(0)
            self.memo.append(cur)
            if cur.left:
                queue.append(cur.left)
            if cur.right:
                queue.append(cur.right)
    
    def insert(self, v: int) -> int:
        n = len(self.memo)
        p_node = self.memo[(n-1)//2]
        if n % 2 == 1: # adds left child
            p_node.left = TreeNode(v)
            self.memo.append(p_node.left)
        else:          # adds right child
            p_node.right = TreeNode(v)
            self.memo.append(p_node.right)
        return p_node.val
        
    def get_root(self) -> TreeNode:
        return self.root
```

#### Complexity

- Time: construction -- `O(n)`, insert -- `O(1)`, get_root -- `O(1)`
- Space: `O(n)`