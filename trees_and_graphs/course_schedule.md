# Course Schedule

#### Description

Given n courses (labeled from 0 to n-1) and pairs of a course and prerequisite,
find whether all courses can be finished or not. If yes, return True. Otherwise, return False.

The pair of the course and prerequisite is, for example, `[0, 1]`, which means: to finish course 0, couse 1 is the prerequisite.

#### Example 1

Input: `n = 2, prerequisites = [[1, 0]]`

Output: `True`

Explanation: Take course 0, then course 1. All courses finish.

#### Example 2

Input: `n = 2, prerequisites = [[1, 0], [0, 1]]`

Output: `False`

#### How to Solve

This is a graph problem. First, build a graph, then, traverse the graph. The traversing will be a topological sort. While constructing a graph, count in-degrees. Start the traverse from in-degree 0 node. In addition to the in-degree 0 nodes, if all nodes could traverse, the answer is True.

#### Solution

- Python

```python
class CourseSchedule:
    def canFinish(self, numCourses: int, prerequisites: 'List[List[int]]') -> bool:
        graph = {i: [] for i in range(numCourses)}
        in_degree = [0 for _ in range(numCourses)]
        for cur, pre in prerequisites:
            graph[pre].append(cur)
            in_degree[cur] += 1
        finished = [i for i in range(numCourses) if in_degree[i] == 0]
        if len(finished) == 0: return False
        for i in finished:
            for c in graph[i]:
                in_degree[c] -= 1
                if in_degree[c] == 0:
                    finished.append(c)
        return numCourses == len(finished)
```

#### Complexity

- Time: O(n^2) -- n is a number of courses
- Space: O(n)