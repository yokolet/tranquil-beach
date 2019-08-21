# One Edit Distance

#### Description

Given two strings `s` and `t`, find whether those are on edit distance apart each other or not.

- Definition

    The following three are possible one edit distance:
    - Insert a character into `s` to get `t`
    - Delete a character from `s` to get `t`
    - Replace a character of `s` to get `t`

#### Example 1

Input: `s = "ab", t = "acb"`

Output: `True`

#### Example 2

Input: `s = "cab", t = "ad"`

Output: `False`

#### Example 3

Input: `s = "1203", t = "1213"`

Output: `True`

#### How to Solve

Some kinds of approches are there to solve this problem. Two pointers may be one of them. The solution here uses the breadth first search (BSF) apporach. A combination of two words and an edit distance so far is saved in a queue. As the words cutting down one by one, the edit distance increase one by one if not match. When two partial words are the same and the edit distance is 1, return true. If the edit distance exceeds 1, return false.

#### Solution

- Python

```python
class OneEditDistance:
    def isOneEditDistance(self, s: str, t: str) -> bool:
        seen = set()
        queue = [(s, t, 0)]
        while queue:
            w1, w2, d = queue.pop(0)
            if d > 1: return False
            if w1 == w2:
                if d == 1: return True
                else: return False
            if (w1, w2) in seen:
                continue
            seen.add((w1, w2))
            while w1 and w2 and w1[0] == w2[0]:
                w1 = w1[1:]
                w2 = w2[1:]
            queue.append((w1, w2[1:], d+1))
            queue.append((w1[1:], w2, d+1))
            queue.append((w1[1:], w2[1:], d+1))
```

#### Complexity

- Time: `O(m+n)` -- m, n are the length of s and t respectively
- Space: `O(m+n)`