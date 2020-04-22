# Split Array Largest Sum

#### Description

Given an array of non-negative integers and an integer `m`, find the minimized largest sum among `m` subarrays after splitting the array into `m` non-empty coninuous subarrays.

#### Example

Input: `[7,2,5,10,8], m = 2`

Output: `18`

Explanation: The largest sum is 18 when the array is split in a way each group's sum is minimuzed.

```
subarray   nums
0          7,2,5
1          10,8
```

#### How to Solve

The binary search is an approach taken here.
The optimal sum exists between maximum value (or average value if average is bigger) and sum of all values. Initial low and high values are those two. Summing up values while the sum doesn't exceed the middle value.
If exceeds, count up the groups (number of groups) and set the sum to the value of that point.
In the end, if the number of groups exceeds the given value `m`, the middle value is considered small. So, set the low as middle value + 1. If the days are less than or equal to the `m`, the middle value is considered big.
So, set the high as middle value. 

- Similar problems
    - [Capacity To Ship Packages Within D Days](package_shipping.md)
    - [Divide Chocolate](divide_chocolate.md)

#### Solution

- Python

```python
class SplitArray:
    def splitArray(self, nums: 'List[int]', m: int) -> int:
        low, high = max(max(nums), sum(nums)//m), sum(nums)
        while low < high:
            mid = (low + high) // 2
            g_sum = 0
            groups = 1
            for v in nums:
                g_sum += v
                if g_sum > mid:
                    g_sum = v
                    groups += 1
            if groups > m:
                low = mid + 1
            else:
                high = mid
        return low
```

#### Complexity

- Time: `O(nlog(s))` -- s is the length of maximum value (or average value if the average is bigger) to sum of values. n is a length of the given array.
- Space: `O(1)`