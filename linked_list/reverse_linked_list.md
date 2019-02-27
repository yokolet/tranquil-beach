# Reverse Linked List

#### Description

Reverse a singly linked list.

#### Example
Input: `1->2->3->4->5->None`

Output: `5->4->3->2->1->None`

#### How to Solve

While iterating to the end, the cur pointer keeps tracking original linked list. The prev pointer keeps tracking a new linked list. The line, `cur.next = prev`, saves a current node. 
The line, `prev = cur`, moves the new linked list pointer forward.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class ReverseLinkedList:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return head
        prev, cur, next_ = None, head, None
        while cur:
            next_ = cur.next
            cur.next = prev
            prev = cur
            cur = next_
        return prev
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
  prev, cur = nil, head
  while cur
    next_ = cur.next
    cur.next = prev
    prev = cur
    cur = next_
  end
  prev
end
```

#### Complexity
- Time: O(n)
- Space: O(1)