# Copy List with Random Pointer

#### Description

Given a linked list whose nodes contain an additional random pointer, return a deep copy of the list.

The random pointer could point to any node in the list or null.

#### Example
Input:

```
{"$id":"1","next":{"$id":"2","next":None,"random":{"$ref":"2"},"val":2},"random":{"$ref":"2"},"val":1}
```

```
val     1        2
next    2   ---> None 
random  2   ---> 2 -+
                 ^  |
                 |  |
                 +--+
```

#### How to Solve

For the first traverse, create linked list with random pointer to None. While creating a new node, save it map for the second traverse.

For the second traverse, assign random pointer.

#### Solution
- Python

```python
# Definition for a Node.
class Node:
    def __init__(self, val, next, random):
        self.val = val
        self.next = next
        self.random = random

class CopyWithRandom:
    def copyRandomList(self, head: 'Node') -> 'Node':
        head2 = Node(None, None, None)
        cur = head
        cache = {} # (key, value) = (cur, ref), copied instance
        prev = head2
        while cur:
            n = Node(cur.val, None, None)
            prev.next = n
            cache[cur.val] = n
            prev = n
            cur = cur.next
        cur = head
        cur2 = head2.next
        while cur:
            if cur.random:
                cur2.random = cache[cur.random.val]
            cur = cur.next
            cur2 = cur2.next
        return head2.next
```

#### Complaxity
- Time: O(n)
- Space: O(n)