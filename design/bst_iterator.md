# Binary Search Tree Iterator

#### Description

Implement an iterator over a binary search tree (BST). The iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.
The hasNext() will return true if the next smallest number exists, otherwise, false.

next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
You may assume that next() call will always be valid, that is, there will be at least a next smallest number in the BST when next() is called.

#### Example

```
       7
     /   \
    3     15
        /    \
       9      20
```

```
iterator = BSTIterator(root)
iterator.next()    // return 3
iterator.next()    // return 7
iterator.hasNext() // return true
iterator.next()    // return 9
iterator.hasNext() // return true
iterator.next()    // return 15
iterator.hasNext() // return true
iterator.next()    // return 20
iterator.hasNext() // return false
```

#### How to Solve

Use stack to save nodes on the way to the current smallest node. This should be done in the constructor and `next()` method.

The next smallest in BST is a successor. The successor is the left most node in the right subtree.
So, the `next()` method starts from right child then
goes left, left....

The hasNext method returns whether stack size is o or not.


#### Solution
- Python

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class BSTIterator:
    def __init__(self, root: 'TreeNode'):
        self.stack = []
        while root is not None:
            self.stack.append(root)
            root = root.left

    def next(self) -> int:
        """
        @return the next smallest number
        """
        if self.hasNext():
            node = self.stack.pop()
            cur = node.right
            while cur:
                self.stack.append(cur)
                cur = cur.left
            return node.val

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        return len(self.stack) > 0
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

class BSTIterator
  # creates an instance
  # @param [TreeNode] root
  def initialize(root)
    @stack = []
    while root
      @stack << root
      root = root.left
    end
  end

  # returns the next smallest node value
  # @return [Integer]
  def next()
    if has_next
      node = @stack.pop
      cur = node.right
      while !cur.nil?
        @stack << cur
        cur = cur.left
      end
      return node.val
    end
  end

  # returns whether the next smallest node exists
  # @return [true] if exists
  def has_next()
    @stack.size > 0
  end
end
```

#### Complexity
- Time: O(1)
- Space: O(h) -- h is a height of the tree