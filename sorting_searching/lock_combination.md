# Open the Lock

#### Description

Given a list of `deadends` and target of a 4 circular wheel lock, return the minimum total number of wheel turns (lock rotations) to reach the target. If it's impossible to reach the target, return -1.

Definitions:
- Each wheel has 10 digits, 0, 1, ..., 8, 9.
- 0 can be turned to 1 or 9. 9 can be turned to 8, or 0.
- The lock starts from `0000`.
- The values in `deadends` prohibit any furhther lock rotations.

#### Example 1

Input: `deadends = ["0201","0101","0102","1212","2002"], target = "0202"`

Output: `6`

Explanation: `"0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202"`

#### Example 2

Input: `deadends = ["8888"], target = "0009"`

Output: `1`

Explanation: `"0000" -> "0009"`

#### Example 3

Input: `deadends = ["8887","8889","8878","8898","8788","8988","7888","9888"], target = "8888"`

Output: `-1`

#### Example 4

Input: `deadends = ["0000"], target = "8888"`

Output: `-1`

#### How to Solve

The problem asks the shortest path from the start ("0000") to target, or target to start. The breadth first search (BFS) would be the best approach. The next paths are created only one of 4 digits rotation. Using a queue and check the distance. If the 4 digit combination is in the deadends or already seen, don't go further. If the 4 digit combination is the target (or "0000" if start from target), return the distance.

#### Solution
- Python

```python
class LockCombination:
    def openLock(self, deadends: 'List[str]', target: str) -> int:
        digits = {str(i): [str((i + 1) % 10), str((i - 1) % 10)] for i in range(10)}
        def nextCombinations(s):
            ary = []
            for i in range(4):
                ary += [s[:i]+x+s[i+1:] for x in digits[s[i]]]
            return ary

        if '0000' in deadends: return -1
        seen = set(deadends)
        seen.add(target)
        queue = [(target, 0)]
        while queue:
            cur, steps = queue.pop(0)
            if cur == '0000': return steps
            for d in nextCombinations(cur):
                if d not in seen:
                    seen.add(d)
                    queue.append((d, steps+1))
        return -1
```

#### Complexity
- Time: `O(1)`
- Space: `O(1)`

    [Note] The lock has only 4 slots and possible combinations are `10^4`. The maximum size of deadends is at most `10^4`. All are constants. If those sizes vary, the complexities change to: time - `O(n*digits^n+d)` (n, digits, and d are the length of lock, digits, and deadends respectively), space - `O(digits^n)`.