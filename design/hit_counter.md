# Design Hit Counter

#### Description

Design a hit counter which counts the number of hits received in the past 5 minutes.

- Definition
    - Each function accepts a timestamp parameter (in seconds granularity).
    - Calls are being made to the system in chronological order (monotonically increasing).
    - The earliest timestamp starts at 1.
    - Several hits may arrive roughly at the same time.

#### Example
```python
counter = HitCounter()
# hit at timestamp 1.
counter.hit(1)
# hit at timestamp 2.
counter.hit(2)
# hit at timestamp 3.
counter.hit(3)
# get hits at timestamp 4, should return 3.
counter.getHits(4)
# hit at timestamp 300.
counter.hit(300)
# get hits at timestamp 300, should return 4.
counter.getHits(300)
# get hits at timestamp 301, should return 3.
counter.getHits(301)
```

#### How to Solve

Use a queue to save the timestamps. This is a kind of monotonic increasing queue problem. The values are added up in the queue. When a query comes in, remove previously queued up values while the value is less than some specific value. In this problem the value is the timestamp, and the specific value is `current timestamp - 5 minutes (300 seconds)`. After those values are removed, the length of the queue is the answer of `getHits`.

#### Solution
- Python

```python
class HitCounter:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.timestamps = [] # queue

    def hit(self, timestamp: int) -> None:
        """
        Record a hit.
        @param timestamp - The current timestamp (in seconds granularity).
        """
        self.timestamps.append(timestamp)

    def getHits(self, timestamp: int) -> int:
        """
        Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity).
        """
        while self.timestamps and self.timestamps[0] <= timestamp - 300:
            self.timestamps.pop(0)
        return len(self.timestamps)
```

#### Complexity
- Time: `hit` -- `O(1)`, `getHits` -- `O(n)` -- n is a number of times `hit` method is called.
- Space: `O(n)`
