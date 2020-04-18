# My Calendar

#### Descirption

Design `MyCalendar` class to store non-overlapping events.
The class has a constructor with no argument and a method `book(start int, end: int)`. The event interval is given by `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

When the method, `book` is called, it returns `True` if the event can be booked without causeing a double booking. Otherwise, return `False` and do not store the event.

#### Example

```python
cal = MyCalendar()
cal.book(10, 20) # -> True
cal.book(15, 25) # -> False
cal.book(20, 30) # -> True
```

#### How to Solve

The bisect search is one of solutions to figure out the given event overlaps with the existing one.
Python's bisect_left search returns the insertion point. Given that, the returned index has the event of the same or later start time. If the index is 0, there's no earler event. If  the index is the same as the array length, the given event happens after of all existing.
Compare start and end time for previous and upcoming events. If those don't overlap, add the event to the insertion point.

#### Solution
- Python

```python
import bisect

class MyCalendar:
    def __init__(self):
        self.calendar = []

    def book(self, start: int, end: int) -> bool:
        idx = bisect.bisect_left(self.calendar, (start, end))
        canBook = True
        canBook &= idx == 0 or start >= self.calendar[idx-1][1]
        canBook &= idx == len(self.calendar) or end <= self.calendar[idx][0]
        if canBook:
            self.calendar = self.calendar[:idx] + [(start, end)] + self.calendar[idx:]
            return True
        else:
            return False
```

#### Complexity
- Time: `O(nlog(n))` -- n is a number of `book` method calls
- Space: `O(n)`
