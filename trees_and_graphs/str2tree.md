# Construct Binary Tree from String

#### Description

Given a string consisting of parenthesis and integers,
construct a binary tree.

The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. The integer represents the root's value and a pair of parenthesis contains a child binary tree with the same structure.

If the left child node of parent exists, start from constructing the left child.

#### Example

Input: `"4(2(3)(1))(6(5))"`

Output: a root node of a tree described blow:

```
       4
     /   \
    2     6
   / \   / 
  3   1 5   
```

#### How to Solve

Typical solution is a recersive call.
Starting from the root node, create left child, then right child.
The given string consists of '(', ')', '-', and digits only.
When the character is '(', it is the time to go deeper.
If the character is ')', it is the time to go back.
The characters, '-' and digits, goes to node value.

The tricky part is to keep index consistent.
This solution uses recursive call, so when the call comes back to previous stack, the value in the method argument goes back to
previous one.
To avoid this, this solution returns the index along side of root node.


#### COmplexity

- Time O(n)
- Space O(h) : h is a height of the tree

#### Solution

{% code-tabs %}

{% code-tabs-item title=Python %}
```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Str2Tree:
    def str2tree(self, s: 'str') -> 'TreeNode':
        if not s: return None
        def walk(s, index, size):
            root = TreeNode(None)
            start = index
            while index < size:
                if s[index] == '(':
                    index += 1
                    if root.left == None:
                        root.left, index = walk(s, index, size)
                    else:
                        root.right, index = walk(s, index, size)
                elif s[index] == ')':
                    index += 1
                    return root, index
                elif s[index] == '-':
                    index += 1
                else:
                    while index < size and str.isdigit(s[index]:
                        index += 1
                    root.val = int(s[start:index])
            return root, index
        root, _ = walk(s, 0, len(s))
        return root        
```
{% endcode-tabs-item %}

{% code-tabs-item title=Ruby %}
```ruby
# @param {String} s
# @return {TreeNode}
def self.str2tree(s)
    return nil if s.nil? || s.empty?
    root, _ = self.walk(s, 0, s.size)
    root
end

def self.walk(s, index, size)
    root = TreeNode.new(nil)
    start = index
    while index < size
        if s[index] == "("
        index += 1
        if root.left == nil
            root.left, index = walk(s, index, size)
        else
            root.right, index = walk(s, index, size)
        end
        elsif s[index] == ")"
        index += 1
        return root, index
        elsif s[index] == "-"
        index += 1
        else
        while index < size && s[index] != ")" && s[index] != "(" && s[index] != "-"
            index += 1
        end
        root.val = s.slice(start...index).to_i
        end
    end
    return root, index
end
```
{% endcode-tabs-item %}
{% endcode-tabs %}