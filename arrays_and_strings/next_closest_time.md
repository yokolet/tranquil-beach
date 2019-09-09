# Next Closest Time

#### Description

Given a time represented in the format "HH:MM", create the next closest time reusing the given digits. The same digit can be used multiple times.

All given input strings are valid such as "01:34" or "12:09".

#### Example 1

Input: "19:34"

Output: "19:39"

Explanation: The next closest time using 1, 9, 3 and 4 is 19:39.

#### Example 2

Input: "23:59"

Output: "22:22"

Explanation: The time "23:59" is the last minute of the day. The next day's earlist time using 2, 3, 5 and 9 is 22:22.

#### How to Solve

All possible combinations of time is at most 4^4 = 256, which is `O(1)`.
Given that, generate all valid possible combinations for the first step.
Then, sort the generated times.
If the given time is the last element in sorted times, the first element will be the answer. That's because the first element is the earliest time on the next day.
If the given time is on somewhere in the sorted times,
find the index of the given time, `idx`. The answer is on the `idx+1`.

#### Solution

- Python

```python
class NextClosestTime:
    def nextClosestTime(self, time: str) -> str:
        digits = {time[0], time[1], time[3], time[4]}
        times = [i+j+k+l for i in digits \
                        for j in digits \
                        for k in digits \
                        for l in digits \
                        if "0" <= i+j <= "23" and "0" <= k+l <= "59"]
        times.sort()
        t0 = time.replace(':', '')
        if times[-1] <= t0:
            result = times[0]
        else:
            idx = times.index(t0)
            result = times[idx+1]
        return result[:2] + ':' + result[2:]
```

#### Complexity

- Time: `O(1)` -- all are constant time calculation
- Space: `O(1)`