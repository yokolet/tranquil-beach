# Flood Fill

#### Description

Given an image as 2D array, a starting coordinate (sr, sc) and a new pixcel value, "flood fill" the image. Return the image after the flood fill.

Details:

- The pixel value is from 0 to 65535.
- The flood fill expands 4 directions from the starting coordinate: up, left, right and down.
- Any connected pixel of the same color as the starting coordinate will have a new color.

#### Example
Input:

```
image = [
    [1,1,1],
    [1,1,0],
    [1,0,1]
]
sr = 1, sc = 1, newColor = 2
```

Output:

```
[
    [2,2,2],
    [2,2,0],
    [2,0,1]
]
```

#### How to Solve

The depth first search (DFS) is the approach this solution took. Start from the given coordinate, check 4 neighbors. If the value is the same as an original color of the starting coordinate, update the color with the new value. When the stack becomes empty, the flood fill is over.

#### Solution
- Python

```python
class FloodFill:
    def floodFill(self, image: 'List[List[int]]', sr: int, sc: int, newColor: int) -> 'List[List[int]]':
        if not image or not image[0]: return []
        m, n, color = len(image), len(image[0]), image[sr][sc]
        if color == newColor: return image
        stack = [[sr, sc]]
        image[sr][sc] = newColor
        while stack:
            cur_r, cur_c = stack.pop()
            for i, j in [[cur_r-1, cur_c], [cur_r, cur_c-1], [cur_r, cur_c+1], [cur_r+1, cur_c]]:
                if 0 <= i < m and 0 <= j < n and image[i][j] == color:
                    image[i][j] = newColor
                    stack.append([i, j])
        return image
```

- Ruby

```ruby
# @param {Integer[][]} image
# @param {Integer} sr
# @param {Integer} sc
# @param {Integer} new_color
# @return {Integer[][]}
def flood_fill(image, sr, sc, new_color)
  return [] if image.nil? || image.empty? || image[0].empty?
  m, n, color = image.size, image[0].size, image[sr][sc]
  return image if color == new_color
  stack = [[sr, sc]]
  image[sr][sc] = new_color
  while !stack.empty?
    cur_r, cur_c = stack.pop
    [[cur_r-1, cur_c], [cur_r, cur_c-1], [cur_r, cur_c+1], [cur_r+1, cur_c]].each do |i, j|
      if 0 <= i && i < m && 0 <= j && j < n && image[i][j] == color
        image[i][j] = new_color
        stack.push([i, j])
      end
    end
  end
  image
end
```

#### Complexity
- Time: O(n) -- n is a number of pixels in the image
- Space: O(n)