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

An easy way is to shift a starting node so that
two linked lists have the same length.
Then, use two pointers -- one for each -- and move two pointers forward at the same time. 
If the lists intersect, two pointers come to the same node.
If the lists don't intersect, two pointers come to None.
Either the intersection exists or not, one of the pointer's value is the answer.

#### Solution

{% code-tabs %}

{% code-tabs-item title="Python" %}
```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Intersection:
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None:
            return None
        
        curA, curB, lenA, lenB = headA, headB, 0, 0
        while curA is not None:
            lenA += 1
            curA = curA.next
        while curB is not None:
            lenB += 1
            curB = curB.next
        
        curA, curB = headA, headB
        if lenA > lenB:
            for _ in range(lenA-lenB):
                curA = curA.next
        elif lenB > lenA:
            for _ in range(lenB-lenA):
                curB = curB.next
        
        while curA != curB:
            curA = curA.next
            curB = curB.next
        return curA
```
{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}
```ruby

```
{% endcode-tabs-item %}

{% endcode-tabs %}

#### Complexity
- Time: O(n)
- Space: O(1)
