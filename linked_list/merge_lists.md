# Merge k Sorted Lists

#### Description

Given k sorted linked lists, return one sorted list by merging them.

#### Example
Input:
```
[
  1->4->5,
  1->3->4,
  2->6
]
```

Output: `1->1->2->3->4->4->5->6`

#### How to Solve

Merge all lists to form one while saving values in a auxiliary array. The merged list has the same number of nodes as the total nodes of the given lists.
Sort values and set those to the merged list one by one.

#### Solution
- Python

```python
class MergeLists:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = ListNode(None)
        cur = head
        values = []
        for list_ in lists:
            while list_:
                cur.next = list_
                values.append(list_.val)
                list_ = list_.next
                cur = cur.next
        cur = head.next
        for v in sorted(values):
            cur.val = v
            cur = cur.next
        return head.next
```

- Ruby

```ruby
# @param {ListNode[]} lists
# @return {ListNode}
def merge_k_lists(lists)
  head = ListNode.new(nil)
  cur = head
  values = []
  lists.each do |list|
    while list
      cur.next = list
      values << list.val
      cur = cur.next
      list = list.next
    end
  end
  cur = head.next
  values.sort().each do |v|
    cur.val = v
    cur = cur.next
  end
  head.next
end
```

#### Complexity
- Time: O(nlog(n)) -- n is the total number of list nodes
- Space: O(n)