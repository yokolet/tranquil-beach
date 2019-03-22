# Reorder List

#### Description

Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

Each node's value should not be modified. Each node's next node can be changed.

#### Example 1
Input: `1->2->3->4`

Reordered: `1->4->2->3`

#### Example 2
Input: `1->2->3->4->5`

Reordered: `1->5->2->4->3`

#### How to Solve

The solution here takes 3 steps. The first step finds a half point in the given linked list. The second step reverses the last half of the linked list. The third step merges first half and reversed last half.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class ReorderList:
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if not head: return
        slow, fast = head, head
        while fast and fast.next: # find half point
            slow, fast = slow.next, fast.next.next
        rev, cur, tmp = None, slow.next, None
        slow.next = None
        while cur: # reverse last half
            tmp = cur.next
            cur.next = rev
            rev = cur
            cur = tmp
        cur = head
        while rev:
            tmp, tmp2 = cur.next, rev.next
            cur.next = rev
            rev.next = tmp
            cur = tmp
            rev = tmp2
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
# @return {Void} Do not return anything, modify head in-place instead.
def reorder_list(head)
  return if head.nil?
  slow, fast = head, head
  while fast && fast.next # find half point
    slow = slow.next
    fast = fast.next.next
  end
  rev, cur, tmp = nil, slow.next, nil
  slow.next = nil
  while cur # reverse last half
    tmp = cur.next
    cur.next = rev
    rev = cur
    cur = tmp
  end
  cur = head
  while rev
    tmp, tmp2 = cur.next, rev.next
    cur.next = rev
    rev.next = tmp
    cur = tmp
    rev = tmp2
  end
end
```

#### Complexity
- Time: O(n)
- Space:  O(1)