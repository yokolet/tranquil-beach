# Minimum Area Rectangle

#### Description

Given a set of points in the xy-plain, find the minimum area of a rectangle formed from these points. All sides are parallel to the x and y axis.

#### Example 1
Input: `[[1,1],[1,3],[3,1],[3,3],[2,2]]`

Output: `4`

#### Example 2
Input: `[[1,1],[1,3],[3,1],[3,3],[4,1],[4,3]]`

Output: `2`

#### How to Solve

If all points are plotted on the xy-plain, it's not difficult to find the minimum area rectangle.
The key to solve this problem is how to find rectangles efficiently. For this purpose, two dictionaries were used in this solution. One is a mapping from x to a set of y, another is a mapping from y to a set of x.

Starting from x, find y-coordinates from the mapping. Check all combinations of two y values at x as heights.
If two y values have a common x values in the mapping other than the starting x, rectangles are created. Calculate the area and compare to the minimum area so far.

#### Solution

- Python

```python
from collections import defaultdict

class MinRectangle:
    def minAreaRect(self, points: 'List[List[int]]') -> int:
        n = len(points)
        x2y, y2x = defaultdict(set), defaultdict(set)
        for x, y in points:
            x2y[x].add(y)
            y2x[y].add(x)
        if len(x2y) == n or len(y2x) == n: return 0
        min_area = float('inf')
        for x, ys in x2y.items():
            ys = list(ys)
            for i in range(len(ys)-1):
                for j in range(i+1, len(ys)):
                    y1, y2 = ys[i], ys[j]
                    for x2 in (y2x[y1] & y2x[y2] - {x}):
                        area = abs(x-x2) * abs(y1-y2)
                        min_area = min(min_area, area)
        return 0 if min_area == float('inf') else min_area
```

#### Complexity
- Time: `O(n^2)` -- n is a lengrh of points
- Space: `O(n)`