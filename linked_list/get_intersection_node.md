# Get Intersection Node of Two Linked List

#### Description

Given two linked lists, find the node at which the intersection of two linked list begins.
If the two lined lists have no intersection at all, return None (nil or null).

The linked list must retain their original structure after the function returns.
There is no cycle anywhere in two linked lists.
The code should tun in O(n) time an O(1) space complexities.

#### Example1
Input: 
```
A:     a1->a2 \
               +->c1->c2->c3
B: b1->b2->b3 /
```

Output: `c1`

#### Example2
Input: 
```
A: a1->a2->a3            
B: b1->b2
```

Output: `None`

#### How to Solve

The solution saves all nodes of the first linked list in the `set`. While going over the second linked list, if the node is in the `set`, the intersection is found.
When the second traversal comes to the end, and still the same node is not found, there's no intersection.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Intersection:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        if not headA or not headB: return None
        seen = set()
        while headA:
            seen.add(headA)
            headA = headA.next
        while headB:
            if headB in seen:
                return headB
            headB = headB.next
        return None
```

#### Complexity
- Time: `O(m+n)` -- m, n are lengths of linked list A and B respectively.
- Space: `O(m)`
