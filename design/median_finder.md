# Find Median from Data Stream

#### Description

Design a data structure which provides `addNum` and `findMedian` methods.

Methods specifications:

- `addNum`: Adds a given integer value to the data structure.
- `findMedian`: Returns the median of all elements so far. (float)

Reference:

    Median is the middle value in an ordered list. For example:
    
    - `[2, 3, 4]` -> median is`3`
    - `[2, 3, 4, 5]` -> median is `(3 + 4) / 2 = 3.5`

#### Example

```
# initializes
medianFinder = MedianFinder()

# adds 1, which doesn't return any
medianFinder.addNum(1)

# adds 2, which doesn't return any
medianFinder.addNum(2)

# gets a median so far, which returns 1.5
medianFinder.findMedian()  # -> 1.5

# adds 3, which doesn't return any
medianFinder.addNum(3)

# get s a median so far, which returns 2
medianFinder.findMedian()  # -> 2
```

#### How to Solve

A typical solution would be to use two heaps, a min and max heap. The min heap is sorted in ascending order, while the max heap is sorted in descending order. The min heap saves a half of the bigger values. The max headp saves a half of the smaller values. Top values of the min and max heaps are the middle values since those are the biggest of the smaller half and the smallest of the bigger half.

In this solution, the min heap will have the same or one greater number of values than the max heap. If the number of values is odd, find the answer from the min heap. Otherwise, calculate the average from the top of both heaps.

Python's heap has a handy method, `heappushpop`. The method pushes the value in and pops the value after heapified. The solution here uses this method.

#### Solution

- Python

```python
import heapq

class MedianFinder:
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.count = 0
        self.maxheap = [] # smaller values than median
        self.minheap = [] # bigger values than median

    def addNum(self, num: int):
        if len(self.maxheap) == len(self.minheap):
            heapq.heappush(self.minheap,
                           -heapq.heappushpop(self.maxheap, -num))
        else:
            heapq.heappush(self.maxheap,
                           -heapq.heappushpop(self.minheap, num))
        self.count += 1

    def findMedian(self) -> float:
        if self.count % 2 == 1:
            return self.minheap[0]
        else:
            return (-self.maxheap[0] + self.minheap[0]) / 2.0
```

#### Complexity

- Time: addNum: O(log(n)), findMedian: O(1)
- Space: O(n) -- n is the number of values