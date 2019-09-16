# Find All Anagrams in a String

#### Description

Given a string s and a non-empty string p, find all start indices of p's anagrams in s.

Strings consist of lowercase English letters only. The length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

#### Example 1
Input: `s = "cbaebabacd"`, `p = "abc"`

Output: `[0, 6]`

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

#### Example 2
Input: `s = "abab"`, `p = "ab"`

Output: `[0, 1, 2]`

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

#### How to Solve

The sliding window is used to solve this problem.

The first step is to find a character to count mapping for the p. The second step is iterating all characters in the string.

While iterating the string `s`, it maintains a current character to count mapping for the `s`, and left pointer. When i - left + 1 is the same as the length of pattern, check target and counts. If those are the same, an anagrams is found.


#### Solution
- Python

```python
from collections import Counter

class AllAnagrams:
    def findAnagrams(self, s: 'str', p: 'str') -> 'List[int]':
        if len(p) > len(s): return []
        target, counts, left, result = dict(Counter(p)), {}, 0, []

        for i in range(len(s)):
            if s[i] not in target:
                counts, left = {}, i + 1
                continue
            counts[s[i]] = counts.get(s[i], 0) + 1
            if i - left + 1 == len(p):
                if counts == target:
                    result.append(left)
                counts[s[left]] -= 1
                left += 1

        return result
```

- Ruby

```ruby
# @param {String} s
# @param {String} p
# @return {Integer[]}
def find_anagrams(s, p)
  return [] if s.size < p.size
  target = p.split('').reduce({}) {|acc, c| acc.has_key?(c) ? acc[c] += 1 : acc[c] = 1; acc}
  counts, left, result = {}, 0, []
  counts.default = 0
  s.size.times do |i|
    if !target.has_key?(s[i])
      counts, left = {}, i + 1
      next
    end
    counts[s[i]] = counts[s[i]] ? counts[s[i]] + 1 : 1
    if i - left + 1 == p.size
      if counts == target
        result << left
      end
      counts[s[left]] -= 1
      left += 1
    end
  end
  result
end
```

#### Complexity
- Time: `O(m+n)` -- m, n are lenghts of s, p respectively
- Space: `O(m+n)`
