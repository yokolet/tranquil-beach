# Meeting Rooms

#### Description

Given an array of meeting time intervals represents start and end times `[[s1, e1], [s2, e2], ...]`, determine if it is possible to attend all meetings.

#### Example 1
Input: `[[0,30],[5,10],[15,20]]`

Output: `False`

#### Example 2
Input: `[[7,10],[2,4]]`

Output: `True`

#### How to Solve

Sorting the input array by the start time is a key to solve the problem. If the previous end time is greater than next start time, two meetings are overlapped. In this case, return `false`. When the loop reaches to the end, return `True`.

#### Solution
- Python

```python
class MeetingRooms:
    def canAttendMeetings(self, intervals: 'List[List[int]]') -> bool:
        intervals.sort(key=lambda x: x[0])
        prev_e = -1
        for cur_s, cur_e in intervals:
            if prev_e > cur_s: return False
            prev_e = cur_e
        return True
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(1)`
