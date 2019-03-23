# Sort List

#### Description

Given a singly linked list, sort a linked list in O(n log n) time using constant space complexity.

#### Example 1
Input: `4->2->1->3`

Output: `1->2->3->4`

#### Example 2
Input: `-1->5->3->4->0`

Output: `-1->0->3->4->5`

#### How to Solve

The problem requires O(1) space complexity. Given that, the approach would a merge sort. The first step is to divide a linked list into 2 parts. Not to make loop endless, the last node of  the first half should have None (nil) to its next pointer.

Once the list is devided into pieces, merge two lists in a merge sort way.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class SortList:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next: return head
        def merge(l1, l2):
            head_ = ListNode(None)
            l0 = head_
            while l1 and l2:
                if l1.val < l2.val:
                    l0.next, l1 = l1, l1.next
                else:
                    l0.next, l2 = l2, l2.next
                l0 = l0.next
            if l1: l0.next = l1
            elif l2: l0.next = l2
            return head_.next
        slow, fast, prev = head, head, None
        while fast and fast.next:
            slow, fast, prev = slow.next, fast.next.next, slow
        prev.next = None
        return merge(self.sortList(head), self.sortList(slow))
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
def sort_list(head)
  return head if head.nil? || head.next.nil?
  merge =-> (l1, l2) {
    head_ = ListNode.new(nil)
    l0 = head_
    while l1 and l2
      if l1.val < l2.val
        l0.next, l1 = l1, l1.next
      else
        l0.next, l2 = l2, l2.next
      end
      l0 = l0.next
    end
    if l1
      l0.next = l1
    elsif l2
      l0.next = l2
    end
    head_.next
  }
  slow, fast, prev = head, head, nil
  while fast && fast.next
    slow, fast, prev = slow.next, fast.next.next, slow
  end
  prev.next = nil
  merge.call(sort_list(head), sort_list(slow))
end
```

#### Complexity
- Time: O(nlog(n))
- Space: O(1)