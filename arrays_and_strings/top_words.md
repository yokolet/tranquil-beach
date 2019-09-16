# Top K Frequent Words

#### Description

Given a non-empty list of words, return the k most frequent elements. The answer should be sorted by frequency from highest to lowest. If two words have the same frequency, the answer should be sorted by alphabetical order.

#### Example 1
Input: `["i", "love", "leetcode", "i", "love", "coding"], k = 2`

Output: `["i", "love"]`

#### Example 2
Input: `["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4`

Output: `["the", "is", "sunny", "day"]`

#### How to Solve

Count the frequency first, then sort it.
Python's heap sort does exactly this problem requires.
In Ruby, Hash sort can take a custom comparator. This works to solve the problem.

#### Solution
- Python

```python
from collections import defaultdict
import heapq

class TopWords:
    def topKFrequent(self, words: 'List[str]', k: int) -> 'List[str]':
        counts = defaultdict(int)
        for w in words:
            counts[w] += 1
        freq = [(-v, word) for word, v in counts.items()]
        heapq.heapify(freq)
        return [heapq.heappop(freq)[1] for _ in range(k)]
```

- Ruby

```ruby
# @param {String[]} words
# @param {Integer} k
# @return {String[]}
def top_k_frequent(words, k)
  counts = {}
  words.each do |w|
    counts[w] ||= 0
    counts[w] += 1
  end
  counts = counts.sort do |a, b|
    if b.last == a.last
      a.first <=> b.first
    else
      b.last <=> a.last
    end
  end
  counts.map(&:first)[0, k]
end
```

#### Complexity
- Time: `O(nlog(n))`
- Space: `O(n)`
