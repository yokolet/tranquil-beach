# Minimum Meeting Rooms

#### Description

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

#### Example 1

Input: `[[0, 30],[5, 10],[15, 20]]`

Output: 2

#### Example 2

Input: `[[7,10],[2,4]]`

Output: 1

#### How to Solve

Sort start and end times to get all events in sorted order.
Then, just look at how many events overlaps.
This solution doesn't look at sets of start/end time.

If current start is less than current end, increament a count so far.
Then, result (max count) is replaced by a bigger value of the result and the count so far. Then, move on to the next start time.
If the current start is bigger than current end, decrement the count so far. Then, move on to the next end time.
In the end, the result value becomes the minimum rooms needed.

#### Solution
- Python

```python
class MinRooms:
    def minMeetingRooms(self, intervals: 'List[List[int]]') -> int:
        starts = sorted([s for s, e in intervals])
        ends = sorted([e for s, e in intervals])
        i, j = 0, 0
        result, count = 0, 0
        while i < len(intervals) and j < len(intervals):
            if starts[i] < ends[j]:
                count += 1
                i +=1
                result = max(result, count)
            else:
                count -=1
                j +=1
        return result
```

- Ruby

```ruby
# Definition for an interval.
class Interval
  attr_accessor :start, :end
  def initialize(s=0, e=0)
    @start = s
    @end = e
  end
end

# @param {Interval[]} intervals
# @return {Integer}
def min_meeting_rooms(intervals)
  starts = intervals.map{ |x| x.start }.sort!
  ends = intervals.map{ |x| x.end }.sort!
  i, j = 0, 0
  result = 0
  current = 0
  while i < intervals.length
    if starts[i] < ends[j]
      current += 1
      i +=1
      result = [result, current].max
    else
      current -=1
      j +=1
    end
  end
  result
end
```

#### Complexity
- Time: `O(nlog(n))`
- Space: `O(n)`