# Valid Square

#### Description

Given coordinates of four points in 2D space, determine the four points shape a square. The coordinate, `[x, y]`, is an array of two integers. The order of the four points are random.

- Definition of Square
    - It has four equal sides with a positive length
    - All four angles are 90-degrees.

#### Example
Input: `p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]`

Ouput: `True`

#### How to Solve

The difficult part of this promblem is that the order of four points is unknown. A naive approach is to check all distances formed by all possible combinations of two points. This problem gives only four points, so all possible combinations are just six. The bruto force solution still gives a reasonably good performance. However, thinking of the nature of the square, comparisons can be cut down. If the six distances are sorted in reverse order, the first two are diagonals. The rest of four are sides. Check the lengths of those.

#### Solution
- Python

```python
class ValidSquare:
    def validSquare(self, p1: 'List[int]', p2: 'List[int]',
                        p3: 'List[int]', p4: 'List[int]') -> bool:
        def dist(a, b):
            return (a[0]-b[0])*(a[0]-b[0])+(a[1]-b[1])*(a[1]-b[1])

        dists = [dist(p1, p2), dist(p1, p3), dist(p1, p4),
                    dist(p2, p3), dist(p2, p4), dist(p3, p4)]
        dists.sort(reverse=True)
        # 2 diagonals and 4 sides
        if dists[0] != 0 and dists[0] == dists[1] and\
            dists[5] != 0 and dists[5] == dists[2] and\
            dists[5] == dists[3] and dists[5] == dists[4]:
            return True
        else:
            return False
```

#### Complexity
- Time: `O(1)` -- given points are 4 always, so constant
- Space: `O(1)`
