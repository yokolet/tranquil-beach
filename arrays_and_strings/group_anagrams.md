# Group Anagrams

#### Description

Given an array of strings, group anagrams. The order of the result doesn't matter.
All inputs are lowercase strings.

#### Example

Input: `["eat", "tea", "tan", "ate", "nat", "bat"]`

Output:

```
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

#### How to Solve

Create a dictionary to save a pair -- sum of each char's hash value as a key and a list of strings as a value. While going over all given strings, sum up hash values to make the key. Then, add the string to the list of the key.

As the result, return the values only.

#### Solution

- Python

```python
from collections import defaultdict

class GroupAnagrams:
    def groupAnagrams(self, strs: 'List[str]') -> 'List[List[str]]':
        groups = defaultdict(list)
        for s in strs:
            h = 0
            for c in s:
                h += hash(c)
            groups[h].append(s)
        return [v for v in groups.values()]
```

#### Complexity

- Time: `O(n * k)` -- n, k are lengths of the given strings and each string respectively.
- Space: `O(m)` -- m is a length of anagrams