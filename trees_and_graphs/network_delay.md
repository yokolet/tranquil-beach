# Network Delay Time

#### Description

Given a number of network nodes `N`, a list of travel times as directed edges `(u, v, w)` (u: source, v: target, w: time), and the startig node `K`, find how long will it to take for all nodes to receive the signal? If it is impossible, return -1.

#### Example 1

Input: `times = [[2,1,1],[2,3,1],[3,4,1]], N = 4, K = 2`

Output: `2`

Explanation:
```
1 <--- [2] ---> 3 ---> 4
    1       1      1
```

#### Example 2

Input: `times = [[1,2,1],[2,1,3]], N = 2, K = 2`

Output: `3`

Explanation:
```
   1
 ---->
1     [2]
 <----
   3
```

#### Example 3

Input: `times = [[1,2,1],[2,3,2],[1,3,1]], N = 3, K = 2`

Output: `-1`

Explanation:
```
   1        2
1 ---> [2] ---> 3
  ------------>
        1
```
The node 1 will not be visited.

#### How to Solve

The solution here took Dijkstra's shortest path algorithm using heap for the implementation. Start from path 0 and starting node combination. While looping, take the shortest path in the queue. If the shortest path target node is not visited, save the path value as the node's shortest. Then, check all edges from the node. Only if next node is not visited, push the combination of path + path to the next and next node to the heap queue. In the end, if saved path dictionary has the length of given number of nodes, return max value in the paths. Otherwise, return -1.

#### Solution
- Python

```python
from collections import defaultdict
import heapq

class NetworkDelay:
    def networkDelayTime(self, times: 'List[List[int]]', N: int, K: int) -> int:
        graph = defaultdict(list)
        for u, v, w in times:
            graph[u].append((v, w))
        path = {}
        queue = [(0, K)]
        while queue:
            cur_w, cur_n = heapq.heappop(queue)
            if cur_n in path: continue
            path[cur_n] = cur_w
            for next_n, next_w in graph[cur_n]:
                if next_n not in path:
                    heapq.heappush(queue, (cur_w + next_w, next_n))
        return max(path.values()) if len(path) == N else -1
```

#### Complexity
- Time: `O(elog(e))` -- e is a number of edges (length of the given list)
- Space: `O(n+e)` -- n is a number of nodes
