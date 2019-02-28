# Number of Islands

#### Description

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. Assume all four edges of the grid are all surrounded by water.

#### Example 1
Input:

```
11110
11010
11000
00000
```

Output: 1

#### Example 2
Input:

```
11000
11000
00100
00011
```

Output: 3

#### How to Solve

There will be a couple or more solutions.
The solution here uses the union-find algorithm.
To reduce auxiliary space, this solution uses an array to save a previous state.

In this problem, only up and left are the position to look at as the previous state.
If the current position's value is 1, up and left values are checked. The current value will be:

- `up = 0 and left = 0`: a new group number is assigned
- `up = 0 and left is not 0`: left value is assigned
- `up is not 0 and left = 0`: up value is assigned
- `up > left`: left is assigned to minimize UF tree depth
- `up <= left`: up is assigned to minimize UF tree depth

In the end, count number of groups.

#### Solution
- Python

```python
class NumberOfIslands:
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]: return 0

        cols = len(grid[0])
        memo = [0 for _ in range(cols)]
        groups = [0]
        gno = 1
        for row in grid:
            for i in range(cols):
                if row[i] == '0':
                    memo[i] = 0
                    continue
                up = groups[memo[i]]
                tmp = 0 if i == 0 else memo[i - 1]
                left = groups[tmp]
                if up == 0 and left == 0:
                    memo[i] = gno
                    groups.append(gno)
                    gno += 1
                elif up == 0:
                    memo[i] = left
                elif left == 0:
                    memo[i] = up
                elif up > left:
                    groups[up] = left
                    memo[i] = left
                else:
                    # up < left
                    groups[left] = up
                    memo[i] = up
        count = 0
        for i in range(1, len(groups)):
            if i == groups[i]:
                count += 1
        return count
```

- Ruby

```ruby
# @param {Character[][]} grid
# @return {Integer}
def num_islands(grid)
  return 0 if grid.empty? || grid[0].empty?
  cols = grid[0].size
  memo = Array.new(cols, 0)
  groups = [0]
  g_no = 1
  grid.each do |row|
    cols.times do |i|
      if row[i] == '0'
        memo[i] = 0
        next
      end
      up = groups[memo[i]]
      left = i == 0 ? groups[0] : groups[memo[i - 1]]
      if up == 0 && left == 0
        memo[i] = g_no
        groups << g_no
        g_no += 1
      elsif up == 0
        memo[i] = left
      elsif left == 0
        memo[i] = up
      elsif up > left
        groups[up] = left
      else
        groups[left] = up
      end
    end
  end
  count = 0
  (1...groups.size).each do |i|
    if i == groups[i]
      count += 1
    end
  end
  count
end
```

#### Complexity
- Time: O(n*m) -- n: rows, m: cols
- Space: O(m)