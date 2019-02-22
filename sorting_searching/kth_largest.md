# Kth Largest Element in an Array

#### Description

Given an unsorted array of integers and value k, find the kth largest element in the array.

The kth largest element is the kth in the sorted order, not the kth distinct element. The given value k is always 1 ≤ k ≤ array's length.

#### Example 1
Input: `[3,2,1,5,6,4]`, `k = 2`

Output: 5

#### Example 2
Input: `[3,2,3,1,2,4,5,5,6]`, `k = 4`

Output: 4

#### How to Solve

One liner, `sorted(nums)[-k]` (Python), is the simplest solution. It works resonably fast.
However, depends on the values in the given array, more efficient solution exists.

The Python solution here uses min heap data structure.
Only k elements are always in the min heap.
Push first k elements in heap and sort, then iterate rest of elements in the array. Only if the element is bigger than the smallest in the heap, pop the smallest and push the bigger one. This way, the heap holds k largest numbers at the index.
When the rest of the array is iterated over, the answer is the smallest in the heap.

The complexity is still O(nlog(n)), however, actual performance is expected better. Since some elements will be skipped and never be a part of heapify, it is something like O((n-m)log(n-m)), where m is a number of smaller elements than the smallest in the heap at index i. In the example 1, 1 and 4 are skipped.

Ruby doesn't have heap nor priority queue in the standard library, the solution is a one liner.

#### Solution
- Python

```python
import heapq

class KthLargest:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        queue = nums[:k]
        heapq.heapify(queue)
        for v in nums[k:]:
            if v > queue[0]:
                heapq.heapreplace(queue, v)
        return queue[0]
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def find_kth_largest(nums, k)
  nums.sort[-k]
end
```

#### Complexity
- Time: O(nlog(n))
- Space: O(k) (Python), O(n) (Ruby)
