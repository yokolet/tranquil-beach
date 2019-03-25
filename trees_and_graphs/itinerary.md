# Reconstruct Itinerary

#### Description

Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. The itinerary must begin with JFK.

If there are multiple valid itineraries, return the itinerary that has the smallest lexical order when read as a single string. 
All airports are represented by three capital letters (IATA code).
At least, one valid itinerary exists.

#### Example 1
Input: `[["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]`

Output: `["JFK", "MUC", "LHR", "SFO", "SJC"]`

#### Example 2
Input: `[["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]`

Output: `["JFK","ATL","JFK","SFO","ATL","SFO"]`

Explanation: `["JFK","SFO","ATL","JFK","ATL","SFO"]` is a valid itinerary, however, it is larger in lexical order.

#### How to Solve

Construct a graph whoose key is a staring airport and value is an array of destinations. Once the graph is created, sort destinations to get a destination by a lexical order.
After the graph is created, do depth first search (dfs).

This solution takes a recursive dfs approach. If the destination is a graph key and its destination exists, go deeper with the first destination as an argument. If not, the given city is the last place to go or all destinations are processed.

The destination is recorded in reverse order. So, reverse it to return the result.

#### Solution
- Python

```python
from collections import defaultdict

class Itinerary:
    def findItinerary(self, tickets: 'List[List[str]]') -> 'List[str]':
        result = []
        if not tickets: return result

        graph = defaultdict(list)
        for s, d in tickets: graph[s].append(d)
        for key in graph: graph[key] = sorted(graph[key])

        def dfs(city):
            while graph[city]:
                dfs(graph[city].pop(0))
            result.append(city)
        
        dfs("JFK")
        return result[::-1]
```

- Ruby

```ruby
# @param {string[][]} tickets
# @return {String[]}
def find_itinerary(tickets)
  graph = {}
  tickets.each do |src, dst|
    graph[src] ||= []
    graph[src] << dst
  end
  graph.each {|key, val| graph[key] = val.sort }
  result = []
  dfs =-> (city) {
    while graph[city] && !graph[city].empty?
      dfs.call(graph[city].shift)
    end
    result << city
  }
  dfs.call("JFK")
  result.reverse
end
```

#### Complexity
- Time: O(V+Elog(E)) -- V is a number of airports, E is a number of routes
- Space: O(V)