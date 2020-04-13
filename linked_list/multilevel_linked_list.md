# Flatten a Multilevel Doubly Linked List

#### Description

Given a head of a doubly linked list whose node has a child pointer, flatten the linked list so that all nodes appear in a single level, doubly linked list.

If the child pointer is not null, it points another doubly linked list head. The nodes in the child list may have the child pointer. The linked list creates a multilevel data structure.

#### Example 1

Input:
```
1--2--3--4--5--6--null
      |
      7--8--9--10--null
         |
         11--12--null
```

Output:
```
1--2--3--7--8--11--12--9--10--4--5--6
```

#### Example 2

Input:
```
1--2--null
|
3--null
```

Output:
```
1--3--2
```

#### Example 3
Input: null

Output: null

#### How to Solve

The linked list has a shape of binary tree. The depth first search (DFS) traversal fulfills the order of this problem's requirement. Going deeper to the child then going further to the next is the way to traverse. However, how to re-link each node to create a flat linked list needs to be considered. For this reason, previous and current nodes are used to traverse the tree. In a pre-order traversal manner, pointers are re-linked. When the traversal is back from the child node, the pointer to the child should be `None`.

#### Solution
- Python

```python
class Node:
    def __init__(self, val, prev, next, child:
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child

class MultilevelLinkedList:
    def flatten(self, head: Node) -> Node:
        def walk(prev, cur):
            if not cur: return prev
            cur.prev = prev
            prev.next = cur
            succ = cur.next
            tail = walk(cur, cur.child)
            cur.child = None
            return walk(tail, succ)
            
        if not head: return head
        dummy = Node(None, None, head, None)
        walk(dummy, head)
        dummy.next.prev = None
        return dummy.next
```

#### Complexity
- Time: `O(n)` -- n is a number of nodes
- Space: `O(d)` -- d is a depth of the tree
