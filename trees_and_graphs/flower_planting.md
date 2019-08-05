# Flower Planting

#### Description

Given N gardens labeled 1 to N and bidirectional paths of gardens, find a flower types of 1 to 4 for each gardens such that any two gardens connected by a path have different types of flowers.

It is guaranteed each garden has at most 3 paths.

#### Example 1

Input: `N = 3, paths = [[1,2],[2,3],[3,1]]`

Output: `[1,2,3]`

#### Example 2

Input: `N = 4, paths = [[1,2],[3,4]]`

Output: `[1,2,1,2]`

#### Example 3

Input: `N = 4, paths = [[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]`

Output: `[1,2,3,4]`

#### How to Solve

This is a graph coloring problem. When the maximum degree is D, D + 1 is enough to color each node by a different color of its neighbors. In this problem D = 3.

First, create a graph, then traverse the graph 1 to N. While traversing the graph, check neighbors' colors and choose a different color. The solution here uses a set to find a color.

#### Solution

- Python

```python
class FlowerPlanting:
    def gardenNoAdj(self, N: int, paths: 'List[List[int]]') -> 'List[int]':
        g = {i: [] for i in range(N+1)}
        for s, d in paths:
            g[s].append(d)
            g[d].append(s)
        flowers = [0 for i in range(N+1)]
        all_flowers = {1, 2, 3, 4}
        for i in range(1, N+1):
            illegals = {flowers[n] for n in g[i]}
            flowers[i] = (all_flowers - illegals).pop()
        return flowers[1:]
```

#### Complexity

- Time: O(n) -- n is a number of nodes
- Space: O(n)

    The time complexity should be O(n + m) precisely, where n, m are number of nodes and edges respectively. However, in this problem, m is at most 4. It is a constant. For this reason, the time complexity is O(n).