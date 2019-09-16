# Top K Frequent Elements

#### Description

Given a non-empty array of integers, return the k most frequent elements.

1 ≤ k ≤ number of unique elements


#### Example 1
Input: `nums = [1,1,1,2,2,3], k = 2`

Output: `[1,2]`

#### Example 2
Input: `nums = [1], k = 1`

Output: `[1]`

#### How to Solve

Create a count table and sort it by a value. Take top k and return the keys.

Python has a handy class, `Counter`, which provides the feature of counting and returning the top k frequent key, value pairs.

#### Solution
- Python

```python
from collections import Counter

class TopK:
    def topKFrequent(self, nums: 'List[int]', k: int) -> 'List[int]':
        counts = Counter(nums).most_common(k)
        return [k for k, _ in counts]
```

- Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer[]}
def top_k_frequent(nums, k)
  counts = {}
  nums.each do |v|
    counts[v] ||= 0
    counts[v] += 1
  end
  topk = counts.sort_by { |_, v| -v }[0, k]
  topk.map { |kv| kv[0] }
end
```

#### Complexity
- Time: `O(nlog(n))`
- Space: `O(n)`
