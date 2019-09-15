# Permutation in String

#### Description

Given two strings s1 and s2, return True if s2 contains the permutaion of s1 (permutation of s1 is a substring of s2).

#### Example 1

Input: `s1 = "ab" s2 = "eidbaooo"`

Output: `True`

Explanation: s2 contains one permutation of s1 "ba".

#### Example 2

Input: `s1= "ab" s2 = "eidboaoo"`

Output: `False`

#### How to Solve

This problem asks whether an anagram of s1 exists in s2 or not. The first step is to find a character to count mapping for s1. For the second step, take the sliding window approach. While iterating s2, update the current character to count mapping for s2. If the length from left to i is the same as the length of s1, compare both mappings. If those are the same, the permutation is found. If not, count down the character at left index, then increment left.

#### Solution

- Python

```python
from collections import defaultdict

class PermutationCheck:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        target = defaultdict(int)
        for c in s1:
            target[c] += 1
        left, counts = 0, defaultdict(int)
        for i in range(len(s2)):
            if s2[i] not in target:
                counts, left = defaultdict(int), i + 1
                continue
            counts[s2[i]] += 1
            if i-left+1 == len(s1):
                if counts == target: return True
                counts[s2[left]] -= 1
                left += 1
        return False
```

#### Complexity

- Time: `O(m + n)` -- m, n are the lengths of s1 and s2
- Space: `O(m)`