# Campus Bikes

#### Description

Given two 2d coordinate lists for workers and bikes,
assign bikes to workers so that every manhattan distance between a worker and bike is minimized.

- The number of workers (N) and bikes (M):  `1 <= N <= M <= 100`.
- Every coordinates x, y: `0 <= x, y < 1000`.

#### Example 1

Input: `workers = [[0,0],[2,1]], bikes = [[1,2],[3,3]]`

Output: `[1,0]`

Explanation: The worker/bike combinations become below:

```
worker   bike
0        1
1        0
```

#### Example 2

Input: `workers = [[0,0],[1,1],[2,0]], bikes = [[1,0],[2,2],[2,1]]`

Output: `[0,2,1]`

Explanation: The worker/bike combinations become below:

```
worker   bike
0        0
1        2
2        1
```

#### How to Solve

The idea of bucket sort is used to solve this problem.
From the definition, the maximum manhattan distance is 2000, so the auxiliary array of length 2000 is used to put the same distances together.
The combinations of `(worker index, bike index)` are saved in the auxiliary array where index is the manhattan distance. Since the same distance appears multiple times, the auxiliary array's element is an array.

Once all disitances are saved in the auxiliary array, go over it.
For the auxiliary array, iterating from 0 to 2000 means looking at distance from shortest to longest. At each index, check inner array's elements. If worker w hasn't been assigned the bike yet, the ans array has None at the index w. In such a case, update the ans array and add bike b to the used set.

#### Solution

- Python

```python
class CampusBikes:
    def assignBikes(self, workers: 'List[List[int]]', bikes: 'List[List[int]]') -> 'List[int]':
        memo = [[] for _ in range(2001)]
        dist = lambda x, y: abs(x[0]-y[0])+abs(x[1]-y[1])
        for i in range(len(workers)):
            for j in range(len(bikes)):
                memo[(dist(workers[i], bikes[j]))].append((i, j))

        ans, used = [None for i in range(len(workers))], set()
        for d in range(2001):
            for w, b in memo[d]:
                if ans[w] is None and b not in used:
                    ans[w] = b
                    used.add(b)
        return ans
```

#### Complexity

- Time: `O(1)` -- the number of workers, bikes are at most 1000, distances are at most 2000. All are constant.
- Space: `O(1)` -- at most 2000