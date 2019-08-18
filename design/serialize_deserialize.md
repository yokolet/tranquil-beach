# Serialize and Deserialize Binary Tree

#### Description

Design an algorithm to serialize and deserialize a binary tree. The format of the serialized tree can be any. The two method should work as in below:

```python
codec = SerializeDeserialize()
root2 = codec.deserialize(codec.serialize(root))
# root2 should be a copy of root
```

- Definition of the serialization

    Converting a data into a computer langauge neutral, sequence of bits.

#### Example

Input for serialize, Output of deserialize:

```
    1
   / \
  2   3
     / \
    4   5
```

Input for deserialize, Output of serialize:

```
"[1,2,3,null,null,4,5]"
```

#### How to Solve

When serializing the tree, a preorder traversal works. To make the result language neutral, Python's `None` is replaced by a string, `'null'`.
At the end, trailing `'null'` should be eliminated.

When deserializing the string, convert it to array and go over the array following the rule:
- parent index is `i`
- left child index is `2*i+1`
- right child index is `2*i+2`

#### Solution

- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class SerializeDeserialize:
    def serialize(self, root: TreeNode) -> str:
        if not root: return '[]'
        result, queue = [], [root]
        while queue:
            cur = queue.pop(0)
            result.append(str(cur.val) if cur else 'null')
            if cur:
                queue.append(cur.left)
                queue.append(cur.right)
        while result[-1] and result[-1] == 'null':
            result.pop()
        return  '[' + ','.join(result) + ']'

    def deserialize(self, data: str) -> TreeNode:
        if not data or data == '[]': return None
        data = data[1:-1].split(',')
        root = TreeNode(int(data[0]))
        idx, queue = 0, [root]
        while queue:
            cur = queue.pop(0)
            if idx*2+1 < len(data) and data[idx*2+1] != 'null':
                cur.left = TreeNode(int(data[idx*2+1]))
                queue.append(cur.left)
            if idx*2+2 < len(data) and data[idx*2+2] != 'null':
                cur.right = TreeNode(int(data[idx*2+2]))
                queue.append(cur.right)
            idx += 1
        return root
```

#### Complexity

- Time: `O(n)`  -- n is a number of nodes in a tree
- Space: `O(h)` -- h is a height of the tree
