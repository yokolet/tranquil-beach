# Largest Rectangle in Histogram

#### Description

Given non-negative integers representing the histogram's bar heights where the width of each bar is 1, find the largest rectangle area in the histogram.

#### Example

Input: `[2,1,5,6,2,3]`

Output: `10`

Explanation: The largest area is index 2 to 3:

```
  .
6 .       █    
       +---+ 
  .    |█ █|    
  .    |█ █|    
  .    |█ █|  █ 
  . █  |█ █|█ █ 
  . █ █|█ █|█ █ 
0 . . . . . . . .
    0         5
```

#### How to Solve

Use stack to save indices. When the previous height is lower than current, calculate the area and compare to the max area.

#### Solution

- Python

```python
class Histogram:
    def largestRectangleArea(self, heights: 'List[int]') -> int:
        if not heights: return 0
        max_area, stack, n = 0, [], len(heights)
        for i in range(len(heights)):
            while stack and heights[stack[-1]] > heights[i]:
                h = heights[stack.pop()]
                w = i if len(stack) == 0 else i - stack[-1] - 1
                max_area = max(max_area, w * h)
            stack.append(i)
        while stack:
            h = heights[stack.pop()]
            w = n if len(stack) == 0 else n - stack[-1] - 1
            max_area = max(max_area, w * h)
        return max_area
```

#### Complexity

- Time: `O(n)`
- Space: `O(n)`