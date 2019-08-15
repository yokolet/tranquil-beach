# Minimum Window Substring

#### Description

Given a string S and T, find the minimum window in S which will contain all the characters in T in complexity O(n).

If there is no such window in S that covers all characters in T, return the empty string "".

When such window exists, only one unique minimum window in S exists.

#### Example
Input: `S = "ADOBECODEBANC", T = "ABC"`

Output: `"BANC"`

#### How to Solve

As a preparation, save character frequency of T to a dictionary (Hash). Set missing characters as the length of T, and left pointer to 0. While going over the string S, if the character is the dictionary's key and its count is greater than 0, decrement missing. Whatever the character is, decrement count for the character in the dictionary. This is to find a minimum length.

Once missing reaches to 0, check the counts in the dictionary to minimize the length. If the count is negative, the character is not in T. So, take it out from the window by incrementing the count and left pointer. Then, compare `current index - left pointer` to `min_right - min_left`.

Lastly, shift the left pointer by incrementing character count. Also, increment missing since the left pointer is on the index of character in T.

#### Solution
- Python

```python
from collections import defaultdict

class MinWindow:
    def minWindow(self, s: str, t: str) -> str:
        missing, left, min_left, min_right = len(t), 0, 0, float('inf')
        target = defaultdict(int)
        for c in t:
            target[c] += 1
        for right, c in enumerate(s, 1):
            if target[c] > 0:
                missing -= 1
            target[c] -= 1
            if missing == 0:
                while target[s[left]] < 0:
                    target[s[left]] += 1
                    left += 1
                if right - left < min_right - min_left:
                    min_left, min_right = left, right
        return '' if min_right == float('inf') else  s[min_left:min_right]
```

- Ruby

```ruby
# @param {String} s
# @param {String} t
# @return {String}
def min_window(s, t)
  missing, left, min_left, min_right = t.size, 0, 0, s.size
  memo = Hash.new { |h, k| h[k] = 0 }
  t.size.times { |i| memo[t[i]] += 1 }
  s.size.times do |i|
    if memo[s[i]] > 0
      missing -= 1
    end
    memo[s[i]] -= 1
    if missing == 0
      while memo[s[left]] < 0
        memo[s[left]] += 1
        left += 1
      end
      if i - left < min_right - min_left
        min_left, min_right = left, i
      end
      memo[s[left]] += 1
      missing += 1
      left += 1
    end
  end
  return '' if min_right == s.size else s[min_left..min_right]
end
```

#### Complexity
- Time: `O(n)` -- two pointers go over once
- Space: `O(m)` -- m is a lenght of a pattern T
