# Merge Two Sorted Lists

#### Description

Given two sorted linked lists, merge those and return as a new list.

#### Example

Input: `1->2->4`, `1->3->4`

Output: `1->1->2->3->4->4`

#### How to Solve

The solution is either recursive or iterative.

When the recursive approach is taken, the base case is the given list is None. Otherwise, go deeper by l1.next or l2.next depending on the values.

When the iterative approach is take, first, create the dummy node for a head. Go over list node comparing the values. In the end, one of the lists may be left. In such a case, add the leftover in the end.

#### Solution 1

- Python

```python
class MergeTwoLists:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2
        elif not l2: return l1
        elif l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```

#### Complexity 1

- Time: O(m+n) -- m, n are lengths of l1, l2 respectively
- Space: O(1)

#### Solution 2

- Python

```python
class MergeTwoLists:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(None)
        cur = dummy
        while l1 and l2:
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next
            cur = cur.next
        if l1: cur.next = l1
        elif l2: cur.next = l2
        return dummy.next
```

#### Complexity 2

- Time: O(m+n) -- m, n are lengths of l1, l2 respectively
- Space: O(1)