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

Create a dictionary to save a pair of a sorted string as a key and a list of strings. While going over all given strings, sort the string to make a key. Then, add the string to the list of the key.

As the result, return the values only.

#### Solution

- Python

```python
class GroupAnagrams:
    def groupAnagrams(self, strs: 'List[str]') -> 'List[List[str]]':
        groups = {}
        for s in strs:
            key = ''.join(sorted(s))
            if key not in groups:
                groups[key] = []
            groups[key].append(s)
        return [v for _, v in groups.items()]
```

#### Complexity

- Time: O(nklog(k)) -- n, k are lengths of the given strings and each string respectively.
- Space: O(n)