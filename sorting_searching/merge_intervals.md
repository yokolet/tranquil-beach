# Merge Intervals

#### Description

Given a collection of intervals, merge all overlapping intervals.

#### Example 1
Input: `[[1,3],[2,6],[8,10],[15,18]]`

Output: `[[1,6],[8,10],[15,18]]`

#### Example 2
Input: `[[1,4],[4,5]]`

Output: `[[1,5]]`

#### How to Solve

Sort intervals by start time. Compare one by one. If previous end time is less than current start time, add current. If previous end time is greater than or equal to current start time, update previous end time by greater value of previous and current end times.

#### Solution
- Python

```python
class Interval:
    def __init__(self, s=0, e=0):
        self.start = s
        self.end = e

class MergeIntervals:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        intervals.sort(key=lambda x: x.start)
        result = []
        for i in intervals:
            if not result or result[-1].end < i.start:
                result.append(i)
            else:
                result[-1].end = max(result[-1].end, i.end)
        return result
```

- Ruby

```ruby
class Interval
  attr_accessor :start, :end
  def initialize(s=0, e=0)
    @start = s
    @end = e
  end
end

# @param {Interval[]} intervals
# @return {Interval[]}
def merge(intervals)
  intervals.sort! {|x, y| x.start <=> y.start }
  result = []
  intervals.each do |i|
    if result.empty? || result[-1].end < i.start
      result << i
    else
      result[-1].end = [result[-1].end, i.end].max
    end
  end
  result
end
```

#### Complexity
- Time: `O(nlog(n))`
- Space: `O(1)`