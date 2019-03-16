#  Is Graph Bipartite?

#### Description

Given an undirected graph, return true if and only if it is bipartite.

- Definition

    A graph is bipartite if all nodes are devided into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

- Format

    The graph is given in the following form: graph[i] is a list of indexes j for which the edge between nodes i and j exists.  Each node is an integer between 0 and graph.length - 1.  There are no self loops or parallel edges: graph[i] does not contain i, and it doesn't contain any element twice.

#### Example 1
Input: `[[1,3], [0,2], [1,3], [0,2]]`

```
0----1
|    |
|    |
3----2
```

Output: `True`

Explanation: The vertices can be devided into two groups: {0, 2} and {1, 3}

#### Example 2
Input: `[[1,2,3], [0,2], [0,1,3], [0,2]]`

```
0----1
| \  |
|  \ |
3----2
```

Output: `False`

Explanation: The node 0 has three neighbors.

#### How to Solve

This is a vertex coloring problem. When a chromatic number is 2, it is called bipartite. Typical solution is depth first search (DFS). The solution here uses a stack to traverse all vertices.
There may be an island, so the solution starts from iterating all vertices.

To keep tracking what vertices are already visited and whose color, an addional dictionary is used.

#### Solution
- Python

```python
class Bipartite:
    def isBipartite(self, graph: 'List[List[int]]') -> 'bool':
        visited = {}
        for vertex in range(len(graph)):
            if vertex not in visited:
                stack = [vertex]
                visited[vertex] = 0
                while stack:
                    v = stack.pop()
                    for n in graph[v]:
                        if n not in visited:
                            stack.append(n)
                            visited[n] = visited[v] ^ 1
                        elif visited[n] == visited[v]:
                            return False
        return True
```

- Ruby

```ruby
# @param {Integer[][]} graph
# @return {Boolean}
def is_bipartite(graph)
  visited = {}
  graph.size.times do |vertex|
    if !visited.has_key?(vertex)
      stack = [vertex]
      visited[vertex] = 0
      while !stack.empty?
        cur = stack.pop
        graph[cur].each do |neighbor|
          if !visited.has_key?(neighbor)
            stack.push(neighbor)
            visited[neighbor] = visited[cur] ^ 1
          elsif visited[neighbor] == visited[cur]
            return false
          end
        end
      end
    end
  end
  true
end
```

#### Complexitu
- Time: O(V + E) -- V is number of vertices, E is number of edges
- Space: O(V)