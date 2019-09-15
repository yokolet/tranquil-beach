# Task Scheduler

#### Description

Given a char array representing tasks CPU need to do by one interval each and non-negative cooling interval n, find the least number of intervals the CPU will take to finish all the given tasks.

The given array contains capital letters, A-Z, which represent different tasks. The original order doesn't matter to complete tasks.

The non-negative cooling interval, n, means that the same tasks must be at least n intervals apart. If there's no other tasks to be done during cooling interval, the CPU goes idle.

The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].

#### Example
Input: `tasks = ["A","A","A","B","B","B"]`, `n = 2`

Output: `8`

Explanation: `A -> B -> idle -> A -> B -> idle -> A -> B`

#### How to Solve

Since the original order doesn't matter, 

- maximum number of a single task (`max_counts`)
- number of tasks which have the maximum value (`same_counts`)

will be used to find the intervals.

The intervals contain at least, `max_counts * same_counts`. Between tasks, there are `(max_counts - 1) * n` intervals. However, the same counts of other tasks can be done without idling. So, the between intervals will be `(max_counts - 1) * (n - (same_counts - 1))`. Lastly, if the tasks has no duplication, the length of tasks will be the answer. Given that, bigger one will be the final answer.

#### Solution
- Python

```python
from collections import Counter

class Tasks:
    def leastInterval(self, tasks: 'List[str]', n: int) -> int:
        counts = Counter(tasks).most_common()
        max_counts, same_counts = counts[0][1], 0
        for _, v in counts:
            if v == max_counts:
                same_counts += 1
            else:
                break
        intervals = max_counts * same_counts
        intervals += (max_counts - 1) * (n - (same_counts - 1)) # between
        return max(len(tasks), intervals)
```

- Ruby

```ruby
# @param {Character[]} tasks
# @param {Integer} n
# @return {Integer}
def least_interval(tasks, n)
  counts = {}
  tasks.each do |t|
    counts[t] ||= 0
    counts[t] += 1
  end
  counts = counts.values
  max_counts = counts.max
  same_counts = counts.count(max_counts)
  intervals = max_counts * same_counts
  intervals += (max_counts - 1) * (n - (same_counts - 1)) # between
  [tasks.size, intervals].max
end
```

#### Complexity
- Time: O(n)
- Space: O(1) -- the size of `counts` is at most 26