# Isomorphic Strings

#### Description

Given two strings `s` and `t` of the same length, determine if they are isomorphic.

- Definition

    Two strings are isomorphic if the character in `s` can be replaced to get `t`. All occurences of the character must be replaced with another character while preserving the order of the character. No two characters may map to the same character but a character may map to itself.

#### Example 1
Input: `s = "egg", t = "add"`

Output: `True`

#### Example 2
Input: `s = "foo", t = "bar"`

Output: `False`

#### Example 3
Input: `s = "paper", t = "title"`

Output: `True`

#### How to Solve

Use a dictionary to save already seen character replecements and check the character one by one.
If the character in `s` is in the dictionary and the replacement is not the `t` at the same index, return False. If the character in `s` is not in the dictionary and the character in `t` at the same index already exists in the values of the dictionary, return False. Otherwise, save the pair. If all characters are checked, return True.

Alternatively, the succinct solution `return len(set(zip(s, t))) == len(set(s)) == len(set(t))` exists.

#### Solution
- Python

```python
from collections import defaultdict

class Isomorphic:
    def isIsomorphic(self, s: str, t: str) -> bool:
        s2t = {}
        for i in range(len(s)):
            if s[i] in s2t:
                if s2t[s[i]] != t[i]: return False
            elif t[i] in s2t.values(): return False
            else: s2t[s[i]] = t[i]
        return True
```

#### Complexity
- Time: `O(n)` -- n is a length of the given string
- Space: `O(n)`
