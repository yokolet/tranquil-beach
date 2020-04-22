# Divide Chocolate

#### Description

Given, a list of integers, `sweetness`, which represents the sweetness of the chocolate and an integer, `K`, which represents a number of friends, find the minimum total sweetness after the list of integers are divided into `K+1` pieces (`K` cuts) optimally.

#### Example 1

Input: `sweetness=[1,2,3,4,5,6,7,8,9], K=5`

Output: `6`

Explanation: optimal cuts are `[1,2,3], [4,5], [6], [7], [8], [9]`, so the minimum total sweetness is 6.

#### Example 2

Input: `sweetness=[5,6,7,8,9,1,2,3,4], K=8`

Output: `1`

#### Example 3

Input: `sweetness=[1,2,2,1,2,2,1,2,2], K=2`

Output: `5`

Explanation: optimal cuts are `[1,2,2], [1,2,2], [1,2,2]`, so the minimum total sweetness is 5.

#### How to Solve

The binary search is an approach taken here. The optimal sum exists between the minimum and average values. Initial low and high values are those two. Summing up values while the sum doesn't exceed the middle value. If exceeds, count up the cuts and set the sum to 0. After calculating the sum, if the number of cuts exceeds the given value `K`, the middle value is considered small. In this case, set the middle as low. Otherwise, set the middle-1 as high. In the end, the high becomes the answer.

- Similar problems
    - [Split Array Largest Sum](split_array.md)
    - [Capacity To Ship Packages Within D Days](package_shipping.md)

#### Solution
- Python

```python
class DivideChocolate:
    def maximizeSweetness(self, sweetness: 'List[int]', K: int) -> int:
        if len(sweetness) == K+1: return min(sweetness)
        low, high = min(sweetness), sum(sweetness)//(K+1)
        while low < high:
            mid = (low + high + 1) // 2
            s_sum, cuts = 0, 0
            for s in sweetness:
                s_sum += s
                if s_sum >= mid:
                    s_sum = 0
                    cuts += 1
            if cuts > K:
                low = mid
            else:
                high = mid - 1
        return high
```

#### Complexity
- Time: `O(nlog(n))` -- n is a length of the given array
- Space: `O(1)`
