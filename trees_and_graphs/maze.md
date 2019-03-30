# The Maze

#### Description

Given 2D array of 0 or 1 where 0: empty space and 1: wall,
start and destination, find if there's a path from the start to destination following the rule below:

- A ball is in an empty space with walls.
- A ball can roll up, down, left or right through empty spaces
- Unless the ball hit a wall, it won't stop.
- When the ball hit the wall, it changes the direction.
- Assume the 2D array is surrounded by walls.

#### Example 1
Input : `start=(0,4), destination=(4,4), maze=`

```
0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0
```

Output: `True`

#### Example 2
Input : `start=(0,4), destination=(3,2), maze=`

```
0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0
```

Output: `False`

#### How to Solve

BFS is the approach this solution took.
The difference from a typical BFS is the direction doesn't change unless it comes to wall. Because of this requirement, while loop is used to keep going. When it comes to the wall, the visited state is updated, and the position is added to the queue.

#### Solution
- Python

```python
class Maze:
    def hasPath(self, maze: 'List[List[int]]', start: 'List[int]', destination: 'List[int]') -> bool:
        if not maze or not maze[0]: return False
        m, n = len(maze), len(maze[0])
        visited = [[False]*n for _ in range(m)]
        queue = [start]
        visited[start[0]][start[1]] = True
        dirs = [[-1, 0], [0, -1], [0, 1], [1, 0]]
        while queue:
            cur_r, cur_c = queue.pop(0)
            if cur_r == destination[0] and cur_c == destination[1]: return True
            for r, c in dirs:
                i, j = cur_r + r, cur_c + c
                while 0 <= i < m and 0 <= j < n and maze[i][j] == 0:
                    i += r
                    j += c
                i -= r
                j -= c
                if not visited[i][j]:
                    queue.append([i, j])
                    visited[i][j] = True
        return False
```

- Ruby

```ruby
# @param {Integer[][]} maze
# @param {Integer[]} start
# @param {Integer[]} destination
# @return {Boolean}
def has_path(maze, start, destination)
  return false if maze.nil? or maze.empty? or maze[0].empty?
  m, n = maze.size, maze[0].size
  visited = Array.new(m) { Array.new(n, false) }
  queue = [start]
  visited[start[0]][start[1]] = true
  dirs = [[-1, 0], [0, -1], [0, 1], [1, 0]]
  while !queue.empty?
    cur_r, cur_c = queue.shift
    return true if cur_r == destination[0] && cur_c == destination[1]
    dirs.each do |r, c|
      i, j = cur_r + r, cur_c + c
      while i >= 0 && i < m && j >= 0 && j < n && maze[i][j] == 0
        i += r
        j += c
      end
      i -= r
      j -= c
      if !visited[i][j]
        queue << [i, j]
        visited[i][j] = true
      end
    end
  end
  false
end
```

#### Complexity
- Time: O(V+E) -- V is a number of vertices: `m*n`, E is a number of edges: `(m-1)*(n-1)`. This can be re-written by `O(m*n)`
- Space: O(V)