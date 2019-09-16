# Palindrome Linked List

#### Description

Given a singly linked list, determine if it is a palindrome in O(n log n) time using constant space complexity.

#### Example 1
Input: `1->2`

Output: `False`

#### Example 2
Input: `1->2->2->1`

Output: `True`

#### How to Solve

Given O(n) time and O(1) space complexity, this solution takes two steps. The first step is to find a middle node while reversing the first half. The second step is a comparison between reversed first half and last half.

#### Solution
- Python

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class PalindromeList:
    def isPalindrome(self, head: ListNode) -> bool:
        slow, fast, rev = head, head, None
        while fast and fast.next: # find half point while reversing first half
            fast = fast.next.next
            rev, rev.next, slow = slow, rev, slow.next
        if fast:
            slow = slow.next
        while rev: # compare reversed first half and last half
            if rev.val != slow.val: return False
            slow = slow.next
            rev = rev.next
        return True
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
# @return {Boolean}
def is_palindrome(head)
  slow, fast, rev = head, head, nil
  while fast && fast.next # find half point while reversing
    fast = fast.next.next
    rev, rev.next, slow = slow, rev, slow.next
  end
  slow = slow.next if fast
  while rev
    return false if rev.val != slow.val
    rev = rev.next
    slow = slow.next
  end
  true
end
```

#### Complexity
- Time: `O(n)` -- n is a length of a linked list
- Space: `O(1)`
