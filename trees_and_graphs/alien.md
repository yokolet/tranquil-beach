# Alien Dictionary

#### Description

Imagine there is an alien language which uses the latin alphabet. However, the order among letters are unknown. Given a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this alien language. Find the order of letters in the language.

#### Example 1
Input:
```
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```

Output: `"wertf"`

#### Example 2
Input:
```
[
  "z",
  "x"
]
```

Output: `"zx"`

#### Example 3
Input:
```
[
  "z",
  "x",
  "z"
]
```

Output: ""

Explanation: The order has a cycle.

#### How to Solve

Create a graph of characters from the given word order.
Then, do topological sort traversing the graph by depth first search (DFS).

Creating the graph needs some idea. While the same char repeats between previous and current words, it's not clear the character order. When, firstly, different characters appear, the edge is found.

The DFS part is a common graph traverse. However, it returns false when the cycle is detected. When false is returned from DFS, the final result will be `""` (empty string).

#### Solution
- Python

```python
from collections import defaultdict

class Alien:
    def alienOrder(self, words):
        """
        :type words: List[str]
        :rtype: str
        """
        graph = defaultdict(list)
        nodes = set()
        def build():
            prev = words[0]
            for c in prev:
                nodes.add(c)
            for cur in words[1:]:
                for c in cur:
                    nodes.add(c)
                i, j = 0, 0
                while i < len(prev) and j < len(cur):
                    if prev[i] == cur[j]:
                        i += 1
                        j += 1
                    else:
                        graph[prev[i]].append(cur[j])
                        break
                prev = cur

        def dfs(node):
            visiting.add(node)
            for child in graph[node]:
                if child not in visited:
                    if child in visiting: # cycle
                        return False
                    else:
                        if not dfs(child): return False
            visited.add(node)
            result.append(node)
            return True

        build()
        result = []
        visited = set()
        visiting = set()
        for node in list(nodes):
            if node not in visited:
                if not dfs(node):
                    return ""
        return ''.join(result[::-1])
```

- Ruby

```ruby
# @param {String[]} words
# @return {String}
def alien_order(words)
  graph = Hash.new { |h, k| h[k] = [] }
  nodes = Set.new
  build = -> {
    prev = words[0]
    prev.split('').each { |c| nodes << c}
    (1...words.size).each do |i|
      cur = words[i]
      cur.split('').each { |c| nodes << c}
      i, j = 0, 0
      while i < prev.size && j < cur.size
        if prev[i] == cur[j]
          i += 1
          j += 1
        else
          graph[prev[i]] << cur[j]
          break
        end
      end
      prev = cur
    end
  }
  build.call()
  visited, visiting, result = Set.new, Set.new, []
  dfs = -> (node) {
    visiting << node
    graph[node].each do |child|
      if !visited.include?(child)
        if visiting.include?(child) # cycle
          return false
        else
          if !dfs.call(child)
            return false
          end
        end
      end
    end
    visited << node
    result << node
    return true
  }
  nodes.each do |node|
    if !visited.include?(node)
      if !dfs.call(node)
        return ""
      end
    end
  end
  result.reverse.join
end
```

#### Complexity
- Time: `O(n * m)` -- n is number of words, m is a length of each word.

    > The loop for DFS is smaller than `n * m`. Upper bound is `O(n * m)`.

- Space: O(V) -- number of nodes (distinct characters)

Time    O(N*M+V+E)
Space   O(V)

N:number of strings
M: average length of strings
V: number of verteces(distinct characters)
E: number of edges(graph connections)
