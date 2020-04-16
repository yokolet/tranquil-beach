# Evaluate Division

#### Description

Given, division formula with its result values and queries, return the answer to the queries. If answer doesn't exist, return -1.0 for the query.

- Definition
    - The division formula is given in the format: `A / B = k`.
    - `A` and `B` are given as strings. `k` is a real number.
    - The given input is always valid. No division by zero exists.

#### Example

Input:
```
equations = [["a","b"],["b","c"]]
values = [2.0, 3.0]
queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
```

Output: `[6.0,0.5,-1.0,1.0,-1.0]`

#### How to Solve

The problem is the weighted directed graph traversal.
```
a -- 2.0 --> b -- 3.0 --> c
```
Apparently, `b / a = 1 / 2.0` when `a / b = 2.0`. So, adding reverse direction:

```
   -- 2.0 -->    -- 3.0  --> 
a              b             c
  <-- 1/2.0 --  <-- 1/3.0 --
```
Additionally, `a / a = 1.0` always.
Given that, the self loop should be added to create a graph.

To find an answer to each query, traverse the graph by the breadth first search (BSF). While traversing, the edge weight is a multiplication of the previous and current values. If it could reach to the destination, return the multiplied edge weight. Otherwise, return -1.0. 

#### Solution
- Python

```python
from collections import deque

class EvaluateDivision:
    def calcEquation(self, equations: 'List[List[str]]',
                            values: 'List[float]',
                            queries: 'List[List[str]]') -> 'List[float]':
        def buildGraph():
            g = {}
            for i in range(len(equations)):
                s, d, v = equations[i][0], equations[i][1], values[i]
                if s not in g:
                    g[s] = [(s, 1)]
                if d not in g:
                    g[d] = [(d, 1)]
                g[s].append((d, v))
                g[d].append((s, 1/v))
            return g

        def search(s, d):
            if s not in graph or d not in graph:
                return -1.0
            queue = deque([(s, 1)])
            seen = {s}
            while queue:
                cur_n, cur_v = queue.popleft()
                for next_n, next_v in graph[cur_n]:
                    if next_n == d: return cur_v * next_v
                    elif next_n not in seen:
                        seen.add(next_n)
                        queue.append((next_n, cur_v * next_v))
            return -1.0

        graph = buildGraph()
        return [search(s, d) for s, d in queries]
```

#### Complexity
- Time: `O(n+m)` -- n and m are a number of nodes and edges respectively
- Space: `O(n)`
