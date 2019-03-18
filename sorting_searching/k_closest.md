# K Closest Points to Origin

#### Description

Given a list of points on the plane, find the K closest points to the origin (0, 0).

The distance between two points on a plane is the Euclidean distance.
The answer is guaranteed to be unique (except for the order that it is in).

#### Example 1
Input: `points = [[1,3],[-2,2]], K = 1`

Output: `[[-2,2]]`

#### Example 2
Input: `points = [[3,3],[5,-1],[-2,4]], K = 2`

Output: `[[3,3],[-2,4]]`
(The answer `[[-2,4],[3,3]]` would also be accepted.)

#### How to Solve

Sort given points [x, y] by x^2 + y^2 and take k smallests.

There would be solution by divide and conquer. However, as fas as tested, this simple solution ran fast enough.

#### Solution
- Python

```python
class KClosest:
    def kClosest(self, points: 'List[List[int]]', K: int) -> 'List[List[int]]':
        return list(sorted(points, key=lambda x: x[0]*x[0]+x[1]*x[1]))[:K]
```

- Ruby

```ruby
# @param {Integer[][]} points
# @param {Integer} k
# @return {Integer[][]}
def k_closest(points, k)
  points.sort_by {|point| point[0]**2 + point[1]**2}[0, k]
end
```

#### Complexity
- Time: O(nlog(n))
- Space: O(n)