# Capacity To Ship Packages Within D Days

#### Description

Given an array of integers and an integer which represents weight of packages and days respectively, find a minimum capacity to ship packages within the given days.

#### Example 1

Input: `weights = [1,2,3,4,5,6,7,8,9,10], D = 5`

Output: `15`

Explanation:

```
day   packages
1     1,2,3,4,5
2     6,7
3     8
4     9
5     10
```

#### Example 2

Input: `weights = [3,2,2,4,1,4], D = 3`

Output: `6`

Explanation:

```
day   packages
1     3,2
2     2,4
3     1,4
```

#### Example 3

Input: `weights = [1,2,3,1,1], D = 4`

Output: `3`

Explanation:

```
day   packages
1     1
2     2
3     3
4     1,1
```

#### How to Solve

The binary search is an approach taken here.
The capacity exists between maximum weight (or average weight if average is bigger) and sum of all weights. Initial low and high values are those two. Summing up weights while the sum doesn't exceed the middle value.
If exceeds, count up the days and set the sum to the weight of that point.
In the end, if days exceeds the given value `D`, the middle value is considered small. So, set the low as middle value + 1. If the days are less than or equal to the `D`, the middle value is considered big.
So, set the high as middle value. 

#### Solution

- Python

```python
class PackageShipping:
    def shipWithinDays(self, weights: 'List[int]', D: int) -> int:
        low, high = max(max(weights), sum(weights)//D), sum(weights)
        while low < high:
            mid = (low + high) // 2
            w_sum = 0
            days = 1
            for w in weights:
                w_sum += w
                if w_sum > mid:
                    w_sum = w
                    days += 1
            if days > D:
                low = mid + 1
            else:
                high = mid
        return low
```

#### Complexity

- Time: `O(log(n))` -- n is the length of maximum weight (or average weight if the average is bigger) to sum of weights
- Space: `O(1)`