# Interval List Intersections

#### Description

Given two sorted lists of closed intervals, where each list of intervals is pairwise disjoint, find the intersection of these two interval lists.

#### Example

Input: `A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]`

Output: `[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]`

#### How to Solve

Take one from each lists and find max start and min end of those. If `start < end`, add the pair to the result list. Take next interval from the list whose current end time is smaller. If the end time is the same for two, both should take next intervals.

#### Solution

- Python

```python
class IntervalIntersection:
    def intervalIntersection(self, A: 'List[List[int]]', B: 'List[List[int]]') -> 'List[List[int]]':
        if not A or not B: return []
        i, j, result = 0, 0, []
        while i < len(A) and j < len(B):
            cur_a, cur_b = A[i], B[j]
            start, end = max(cur_a[0], cur_b[0]), min(cur_a[1], cur_b[1])
            if start <= end:
                result.append([start, end])
            if cur_a[1] == cur_b[1]:
                i += 1
                j += 1
            elif cur_a[1] < cur_b[1]:
                i += 1
            else:
                j += 1
        return result
```

#### Complexity

- Time: `O(n)` -- n is a length of shorter array.
- Space: `O(1)`