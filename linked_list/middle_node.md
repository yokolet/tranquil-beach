# Middle of the Linked List

#### Description

Give a non-empty, singly linked list, return a middle node of the linked list. If there are two middle nodes, return the second middle node.

#### Example 1

Input: `1 -> 2 -> 3 -> 4 -> 5`

Output: `3` (serialized form: `3 -> 4 -> 5`)

#### Example 2

Input: `1 -> 2 -> 3 -> 4 -> 5 -> 6`

Output: `4` (serialized form: `4 -> 5 -> 6`)

#### How to Solve

Use two pointers, slow and fast. The slow pointer goes forward one by one, while the fast pointer goes forward two. When the fast poister reaches to the end, the slow pointer is on the middle node.

Whether the length of the linked list is even or odd, the loop stays the same. When the length is odd, the fast pointer is on the last node. When the length is even, the fast pointer is on the next of the last node. Both cases, the slow pointer is on the middle.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class MiddleNode:
    def middleNode(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```

#### Complexity
- Time: `O(n)` -- n is a length of the linked list
- Space: `O(1)`
