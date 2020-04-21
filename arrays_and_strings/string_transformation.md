# String Transforms Into Another String

#### Description

Given two strings of the same length, `str1` and `str2`, determine whether `str1` can transform into `str2` by doing zero or more conversions. Return `True` if and only if it is possible.
In one conversion, all occurence of one character in `str1` will be convert to any other lowercase English character.

#### Example 1

Input: `str1 = "aabcc", str2 = "ccdee"`

Output: `True`

Explanation: aabcc -> aabee -> aadee -> ccdee

#### Example 2

Input: `str1 = "leetcode", str2 = "codeleet"`

Output: `False`

#### Example 3

Input: `str1 = "abcdefghijklmnopqrstuvwxyz", str2 = "bcdefghijklmnopqrstuvwxyza"`

Output: `False`

#### How to Solve

If the two strings are the same, the answer is True.
If `str2` has 26 types of characters (a-z), there is no character to save intermediate conversion state. In this case, return False.
Otherwise go over each character in str1 and str1. When unseen character in str1 is found, make a pair of the characters of the same index of str1 and str2. When already seen character appears, check the pair is still the same. If not, return False. When it reaches to the last character and still the pair is the same, return True.

#### Solution
- Python

```python
class StringTransformation:
    def canConvert(self, str1: str, str2: str) -> bool:
        if str1 == str2: return True
        if len(set(str2)) == 26: return False
        pair = {}
        for c1, c2 in zip(str1, str2):
            if c1 not in pair:
                pair[c1] = c2
            elif pair[c1] != c2:
                return False
        return True
```

#### Complexity
- Time: `O(n)` -- n is a length of given strings
- Space: `O(1)` -- constant since the pairs are at most 26
