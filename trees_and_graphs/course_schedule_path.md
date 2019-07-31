# Course Schedule Path

#### Descripton

Given n courses (labeled from 0 to n-1) and pairs of a course and prerequisite,
find the ordering (array) of courses to finish all.

The pair of the course and prerequisite is, for example, `[0, 1]`, which means: to finish course 0, couse 1 is the prerequisite.

For some cases, multiple correct orders exist. Return one of them. If there's no way to finish all courses, return an empty array.

#### Example 1

Input: `2, [[1, 0]]`

Output: `[0, 1]`

#### Example 2

Input: `4, [[1,0],[2,0],[3,1],[3,2]]`

Output: `[0, 1,2, 3] or [0, 2, 1, 3]`

#### How to Solve

This is a graph problem. First, build a graph, then, traverse the graph. The traversing will be a topological sort. Start from not yet visited node, do the depth first search (DFS). Since the loop is possible, use 3 state, not visited, visiting, and visited. When all deeper nodes were visited, add the node value to the course order list.

#### Solution

- Python

```python
class CourseSchedulePath:
    def findOrder(self, numCourses: int, prerequisites: 'List[List[int]]') -> 'List[int]':
        graph = {i: [] for i in range(numCourses)}
        for req in prerequisites:
            graph[req[0]].append(req[1])

        def topSort(node):
            if visited[node] != 0: return visited[node]
            visited[node] = 1 # visiting
            for c in graph[node]:
                if topSort(c) == 1:
                    return 1
            result.append(node)
            visited[node] = 2 # visited
            return 0

        result = []
        visited = [0 for _ in range(numCourses)] # all are not yet visited
        for i in range(numCourses):
            if visited[i] == 0:
                if topSort(i) == 1:
                    return []
        return result
```

#### Complexity

- Time: O(m+n) -- m, n are lengths of nodes and edges
- Space: O(m)