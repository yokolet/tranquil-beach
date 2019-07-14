# Reverse Linked List Between m to n

#### Description

Reverse a linked list from position m to n.

- should be done in O(n) time complexity.
- 1 ≤ m ≤ n ≤ [length of linked list].

#### Example

Input: `1->2->3->4->5->NULL, m = 2, n = 4`

Output: `1->4->3->2->5->NULL`

#### How to solve

A basic idea is the same as reversing whole linked list.
However, in this case, the pointer needs to be shifted by m before the reversal. Also, reversing should be ended at n. A tricky part is, the reversed head and tail should be linked to the rest of the linked list.

The solution here stops shifting the pointer at m-1. The position is the tail of left portion. Starting from the node m-1,
the code reverses one by one. While reversing, `cur.next.next` is kept tracking since it will be the head of right portion.

Just in case, m is pointing the first node, a dummy node will be created at the beginning.

#### Solution

- Python

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class ReverseLinkedListRange:
    def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        if not head or m == n: return head
        cur = dummy = ListNode(None)
        dummy.next = head
        for _ in range(m - 1):
            cur = cur.next
        prev, cur, next_ = cur, cur.next, None
        for _ in range(m, n):
            next_ = cur.next
            cur.next = cur.next.next
            next_.next = prev.next
            prev.next = next_
        return dummy.next
```

#### Complexity

- Time: O(n)  -- n is the end node position to reverse
- Space: O(1)
