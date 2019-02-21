# Add Two Numbers

#### Description

Given two non-empty linked lists representing two non-negative integers,
add the two numbers and return it as a linked list.

The digits in the linked list are stored in reverse order and each of
their nodes contain a single digit.
Two numbers do not contain any leading zero, except the number 0 itself.

#### Example
Input: `2 -> 4 -> 3, 5 -> 6 -> 4`

Output: `7 -> 0 -> 8`

Explanation: `342 + 465 = 807`

#### How to Solve

Use two pointers -- one for each linked list, and calculate:

```
v = val1 + val2 + carry
carry = v // 10
remainder = v % 10
```

The remainder goes to the current node value.
A tricky part is lengths of two linked list are not the same.
The solution here doesn't create a new linked list
Instead, the value of the first linked list will be replaced by the remainder.
When the first linked list is shorter than the second, the pointer
goes to the second linked list. In this case, the shape looks like two linked lists are merged at some node.

#### Solution

{% code-tabs %}

{% code-tabs-item title="Python" %}
```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class TwoNumbers:
    def addTwoNumbers(self, l1, l2):
        '''
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        '''
        if not l1 or not l2:
            return l1 or l2
        head = l1
        carry = 0
        while l1 and l2:
            carry, rem = divmod(l1.val + l2.val + carry, 10)
            l1.val = rem
            cur, l1, l2 = l1, l1.next, l2.next
        cur.next = l1 or l2
        while carry != 0:
            if not cur.next:
                cur.next = ListNode(carry)
                break
            else:
                carry, rem = divmod(cur.next.val + carry, 10)
                cur.next.val = rem
                cur = cur.next
        return head
```
{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}
```ruby
class ListNode
  attr_accessor :val, :next

  def initialize(val)
    @val = val
    @next = nil
  end
end

# @param {ListNode} l1
# @param {ListNode} l2
# @return {ListNode}
def add_two_numbers(l1, l2)
  return l1 || l2 if l1.nil? || l2.nil?
  head = l1
  carry = 0
  while l1 && l2
    carry, rem = (l1.val + l2.val + carry).divmod(10)
    l1.val = rem
    cur, l1, l2 = l1, l1.next, l2.next
  end
  cur.next = l1 || l2
  while carry != 0
    if cur.next.nil?
      cur.next = ListNode.new(carry)
      break
    else
      carry, rem = (cur.next.val + carry).divmod(10)
      cur.next.val = rem
      cur = cur.next
    end
  end
  head
end
```
{% endcode-tabs-item %}

{% endcode-tabs %}

#### Complexity
- Time: O(n) -- n is the length of longer linked list
- Space: O(1)
