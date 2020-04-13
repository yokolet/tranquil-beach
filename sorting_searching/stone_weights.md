# Last Stone Weight

#### Description

Given an array of positive integers which represent weights of stones, repeat the operation described below. Return the weight of the last stone or 0 if there is no stone left.

- Rules:
    - choose two heaviest stones, `x` and `y` (`x <= y`)
    - if `x == y`, both stones are destroyed.
    - if `x != y`, `x` is destroyed and `y` will have the new weight of `y - x`.

#### Example

Input: `[2,7,4,1,8,1]`

Output: `1`

Explanation: `[2,7,4,1,8,1]` -> `[2,4,1,1,1]` -> `[2,1,1,1]` -> `[1,1,1]` -> `[1]`

#### How to Solve

The heap is a good data structure to solve this problem. Always two biggest stones are taken out from the array and the difference of two will be added to the array. At the next phase, again the biggest two are taken from the array then differece is added. The heap is a perfect match for this.

Python's heap is always min-heap, so the values are changed to the negative.

#### Solution
- Python

```python
import heapq

class StoneWeights:
    def lastStoneWeight(self, stones: 'List[int]') -> int:
        stones  = [-v for v in stones]
        heapq.heapify(stones)
        while len(stones) > 1:
            a, b = heapq.heappop(stones), heapq.heappop(stones)
            diff = abs(a - b)
            if diff > 0:
                heapq.heappush(stones, -diff)
        return 0 if len(stones) == 0 else -stones[0]
```

#### Complexity
- Time: `O(nlog(n))` -- n is a length of the given array
- Space: `O(1)` -- since the heapify happens in place, it dones't need additional space.
