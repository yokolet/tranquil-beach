# Remove Nth Node From End of List

#### Description

Given a linked list, remove the n-th node from the end and return its head. Given n is always valid.

#### Example
Input: `1->2->3->4->5`, `n = 2`

Output: `1->2->3->5`

#### How to Solve

This is a two-pointer solution. The fast pointer goes over nodes by n at the first. The cur and fast pointer's distance is n. Shift two pointers at the same time. When fast reaches to the end, the cur points one node bofore the node to be removed.
To avoid edge case, the solution adds one extra node before head. The nth node may be the head node. In such a case, extra node works well.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class NthNodeFromEnd:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(None)
        dummy.next = head
        fast = dummy
        for _ in range(n):
            fast = fast.next
        cur = dummy
        while fast.next:
            fast = fast.next
            cur = cur.next
        cur.next = cur.next.next
        return dummy.next
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
# @param {Integer} n
# @return {ListNode}
def remove_nth_from_end(head, n)
  root = ListNode.new(nil)
  root.next = head
  fast = root
  n.times { fast = fast.next }
  cur = root
  while fast.next
    fast = fast.next
    cur = cur.next
  end
  cur.next = cur.next.next
  root.next
end
```

#### Complexity
- Time: `O(n)` -- n is a length of a linked list
- Space: `O(1)`
