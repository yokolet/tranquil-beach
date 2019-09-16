# Reverse Linked List

#### Description

Reverse a singly linked list.

#### Example
Input: `1->2->3->4->5->None`

Output: `5->4->3->2->1->None`

#### How to Solve

While iterating to the end, the cur pointer keeps tracking original linked list. The rev pointer keeps tracking a new linked list. The assignment, `rev = cur`, saves a current node as a reverse head.
The next assignment, `rev.next = rev`, moves the reverse pointer forward.
The last assignment, `cur = cur.next`, moves the original linked list pointer forward.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class ReverseLinkedList:
    def reverseList(self, head: ListNode) -> ListNode:
        cur, rev = head, None
        while cur:
            rev, rev.next, cur = cur, rev, cur.next
        return rev
```

- Ruby

```ruby
class ListNode
  attr_accessor :val, :next

  def initialize(val)
    @val = val
    @next = nil
  end
end

# @param {ListNode} head
# @return {ListNode}
def reverse_list(head)
  return head if head.nil?
  rev, cur = nil, head
  while cur
    next_ = cur.next
    cur.next = rev
    rev = cur
    cur = next_
  end
  rev
end
```

#### Complexity
- Time: `O(n)`  -- n is a lenght of the linked list
- Space: `O(1)`
