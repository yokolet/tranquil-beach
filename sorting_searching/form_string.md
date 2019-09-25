# Shortest Way to Form String

#### Description

Given two strings `source` and `target`, return the minimum number of subsequences of `source` such that their concatenation equals `target`. If the concatanation is impossible, return -1

#### Example 1
Input: `source = "abc", target = "abcbc"`

Output: `2`

Explanation: `"abcbc" = "abc" + "bc"`

#### Example 2
Input: `source = "abc", target = "acdbc"`

Output: `-1`

Explanation: "d" is not in the source

#### Example 3
Input: `source = "xyz", target = "xzyxz"`

Output: `3`

Explanation: `"xzyxz" = "xz" + "y" + "xz"`

#### How to Solve

While iterating over the target string, keep tracking the index of the character in the source. When finding the index, specify the starting index. The starting index should be greater than the last index. If there's no such character, count up and start searching from index 0.

#### Solution

- Python

```python
class FormString:
    def shortestWay(self, source: str, target: str) -> int:
        idx, count = len(source), 0
        for i, c in enumerate(target):
            next_idx = source.find(c, idx+1)
            if next_idx != -1:
                idx = next_idx
                continue
            count += 1
            next_idx = source.find(c, 0)
            if next_idx == -1:
                return -1
            idx = next_idx
        return count
```

#### Complexity
- Time: `O(n)` -- n is a length of target string
- Space: `O(1)`