# Container with Most Water

#### Description

Given an array of non-negative integers, where each element represents a height of a bar at coordinate (i, hi), find maximum water available to save between bars.

#### Example

Input: `[1,8,6,2,5,4,8,3,7]`

Output: `49`

Explanation: `[8,6,2,5,4,8,3,7]` is the maximum of 49

```
8    |              |
7    |              |     |
6    |  |           |     |
5    |  |     |     |     |
4    |  |     |  |  |     |
3    |  |     |  |  |  |  |
2    |  |  |  |  |  |  |  |
1 |  |  |  |  |  |  |  |  | 
  0  1  2  3  4  5  6  7  8 
```

#### How to Solve

An area is calculated by `base * height`. Whether the base is longer or height is taller gives a bigger area. So, the calculation starts from indices of 0 and last -- the base is the longest. Next, move the index of lower height. This will decrease the base, but the minimum height may become taller. Compare the areas and find the maximum.

#### Solution

- Python

```python
class ContainerWater:
    def maxArea(self, height: 'List[int]') -> int:
        left, right, max_water = 0, len(height) - 1, 0
        while left < right:
            min_height = min(height[left], height[right])
            max_water = max(max_water, min_height*(right - left))
            if  height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return max_water
```

#### Complexity

- Time: O(n)
- Space: O(1)