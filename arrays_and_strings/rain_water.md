# Trapping Rain Water

#### Description

Given n non-negative integers representing an elevation map where the width of each bar is 1, find how much water it is able to trap after raining.

#### Example
Input: `[0,1,0,2,1,0,1,3,2,1,2,1]`

Output: `6`

#### How to Solve

Use two pointers to check max height on the left and right sides.
The picture below shows the example above.

```
                                             ┌────┐
3  .                                         │xxxx│
                                             └────┘
                     ┌────┐                  ┌────┐┌────┐      ┌────┐
2  .                 │xxxx│                  │xxxx││xxxx│      │xxxx│
                     └────┘                  └────┘└────┘      └────┘
         ┌────┐      ┌────┐┌────┐      ┌────┐┌────┐┌────┐┌────┐┌────┐┌────┐
1  .     │xxxx│      │xxxx││xxxx│      │xxxx││xxxx││xxxx││xxxx││xxxx││xxxx│
         └────┘      └────┘└────┘      └────┘└────┘└────┘└────┘└────┘└────┘
      .     .     .     .     .     .     .     .     .     .     .     .
      0     1     2     3     4     5     6     7     8     9     10    11 
```

When `left max <= right max`, adds `left max - height[left]` to the total and increment left pointer.
When `left max > right max` adds `right max = height[right]` to the total and decrement right pointer. The table below explains how left/right pointers and total change.

|left,right|0,11|1,11|2,11|3,11|3,10|4,10|5,10|6,10|7,10|7,9|7,8|
| -------- | --:| --:| --:| --:| --:| --:| --:| --:| --:|--:|--:|
|left max  | 0  | 1  | 1  | 2  | 2  | 2  | 2  | 2  | 3  | 3 | 3 |
|right max | 1  | 1  | 1  | 1  | 2  | 2  | 2  | 2  | 2  | 2 | 2 |
|total     | 0  | 0  | 1  | 1  | 1  | 2  | 4  | 5  | 5  | 6 | 6 |

#### Solution
- Python

```python
class RainWater:
    def trap(self, height: 'List[int]') -> int:
        if not height or len(height) < 3: return 0
        left, right, total = 0, len(height) - 1, 0
        left_max, right_max = height[left], height[right]
        while left < right:
            if left_max <= right_max:
                total += left_max - height[left]
                left += 1
                left_max = max(left_max, height[left])
            else:
                total += right_max - height[right]
                right -= 1
                right_max = max(right_max, height[right])
        return total
```

- Ruby

```ruby
# @param {Integer[]} height
# @return {Integer}
def trap(height)
  left, right, total = 0, height.size - 1, 0
  left_max, right_max = height[left], height[right]
  while left < right
    left_max, right_max = [left_max, height[left]].max, [right_max, height[right]].max
    if left_max <= right_max
      total += (left_max - height[left])
      left += 1
    else
      total += (right_max - height[right])
      right -=1
    end
  end
  total
end
```

#### Complaxity
- Time: `O(n)`
- Space: `O(1)`
