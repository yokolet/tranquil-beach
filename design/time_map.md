# Time Based Key-Value Store

#### Description

Design a time based key-value store, `TimeMap`, which supprts the operations below:

- `set(key :str, value :str, timestamp: int)`

    - stores the `key` and `value` along with the given `timestamp`

- `get(key: str, timestamp: int) -> str`

    - returns the `value` of the given `key` whose `timestamp` is less than or equal to the `timestamp` in the argument
    - if multiple timestamps are found, return the `value` of the largest `timestamp` among those
    - if no value matches the condition, return empty string

#### Example 1

```
tm = TimeMap()
tm.set('foo', 'bar', 1)
tm.get('foo', 1)          # returns 'bar'
tm.get('foo', 3)          # returns 'bar' since timestamp 1 is less than 3
tm.set('foo', 'bar2', 4)
tm.get('foo', 4)          # returns 'bar2'
tm.get('foo', 5)          # returns 'bar2'
```

#### Example 2

```
tm = TimeMap()
tm.set('love', 'high', 10)
tm.set('love', 'low', 20)
tm.get('love', 5)            # returns ''
tm.get('love', 10)           # returns 'high'
tm.get('love', 15)           # returns 'high'
tm.get('love', 20)           # returns 'low'
tm.get('love', 25)           # returns 'low'
```

#### How to Solve

The solution takes two dictionaries approach. One saves key-value pairs, another saves key-timestamp pairs. Both, value is an array.

The `set` method sets key-value and key-timestamp pairs. When `get` method gets called, the timestamp array of the key is searched.
The timestamps comes in the ascending order, so binary search will be performed.
Possible matches are: 1. the query timestamp is found, 2. the query timestamp is less than the first value in the timestamp array. 3. the query timestamp is between timestamps in the array.

When appropriate timestamp is found, returns the value of that timestam, otherwise emtpy string.

#### Solution

- Python

```python
from collections import defaultdict

class TimeMap:
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.times = defaultdict(list)
        self.values = defaultdict(list)
        
    def set(self, key: str, value: str, timestamp: int) -> None:
        self.times[key].append(timestamp)
        self.values[key].append(value)

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.times: return ''
        ts = self.times[key]
        if not ts or timestamp < ts[0]: return ''
        low, high = 0, len(ts)-1
        while low <= high:
            mid = (low + high) // 2
            if ts[mid] == timestamp:
                low = high = mid
            if ts[mid] <= timestamp:
                low = mid + 1
            else:
                high = mid - 1
        return self.values[key][high]
```

#### Complexity
- Time: set: `O(1)`, get: `O(log(n))` -- n is a length of timestamps for the key
- Space: `O(k)` -- k is a length of keys