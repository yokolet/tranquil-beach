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

The solution uses Python's defaultdict as a cache.
The default value is an instance of `Node`.
While traversing the given linked list, a pair of the cur node as a key, cur node's value/ref to next and random as a value will be saved in the cache. It is a defaultdict, so the referenced next and random nodes are created for the first reference. For some nodes, actual values for copied node are filled out later. In any case, when the traversal ends, all values are set in the copied linked list.

#### Solution
- Python

```python
# Definition for a Node.
class Node:
    def __init__(self, val, next, random):
        self.val = val
        self.next = next
        self.random = random

from collections import defaultdict

class CopyWithRandom:
    def copyRandomList(self, head: Node) -> Node:
        cache = defaultdict(lambda: Node(None, None, None))
        cache[None] = None  # to avoid if statement in the loop
        cur = head
        while cur:
            cache[cur].val = cur.val
            cache[cur].next = cache[cur.next]
            cache[cur].random = cache[cur.random]
            cur = cur.next
        return cache[head]
```

#### Complaxity
- Time: `O(n)` -- n is a length of a linked list
- Space: `O(n)`