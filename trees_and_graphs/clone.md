# Clone Graph

#### Description

Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a val (`int`) and a list (`List[Node]`) of its neighbors.

#### Example
Input:
```
1 ---- 2
|      |
|      |
4 ---- 3
```
```
{"$id":"1","neighbors":[{"$id":"2","neighbors":[{"$ref":"1"},{"$id":"3","neighbors":[{"$ref":"2"},{"$id":"4","neighbors":[{"$ref":"3"},{"$ref":"1"}],"val":4}],"val":3}],"val":2},{"$ref":"4"}],"val":1}
```

Output: same as input

#### How to Solve

The solution takes BFS (breadth first search). To avoid re-create the same node, it uses a dictionary to look up already created nodes.
Starting the first node in the queue, create a copy node one by one popping out from the queue.
When neighbor nodes are there, add those for upcoming steps.

#### Solution
- Python

```python
# Definition for a Node.
class Node:
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors

class Clone:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node: return None
        head  = Node(node.val, [])
        nodes = {node: head}
        queue = [node]
        while queue:
            cur = queue.pop(0)
            for n in cur.neighbors:
                if n not in nodes:
                    new_node = Node(n.val,[])
                    nodes[n] = new_node
                    nodes[cur].neighbors.append(new_node)
                    queue.append(n)
                else:
                    nodes[cur].neighbors.append(nodes[n])
        return head
```

#### Complexity
- Time: O(n)
- Space: O(n)