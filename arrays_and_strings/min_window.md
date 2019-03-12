# Minimum Window Substring

#### Description

Given a string S and T, find the minimum window in S which will contain all the characters in T in complexity O(n).

If there is no such window in S that covers all characters in T, return the empty string "".

When such window exists, only one unique minimum window in S exists.

#### Example
Input: `S = "ADOBECODEBANC", T = "ABC"`

Output: `"BANC"`

#### How to Solve

As a preparation, save character frequency of T to a dictionary (Hash). Set missing characters as the length of T, and left pointer to 0. While going over the string S, if the character is memo's key and its count is greater than 0, decrement missing. Whatever the character is, decrement count for the character in memo. This is to find a minimum length.

Once missing reaches to 0, check the counts in memo to minimize the length. If the count is negative, the character is not in T. So, take it out from the window by incrementing the count and left pointer. Then, compare `current index - left pointer` to `min_right - min_left`.

Lastly, shift window's left side by incrementing character count and left pointer. Also, increment missing since the left pointer is on the index of character in T.

#### Solution
- Python

```python
class MinWindow:
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        missing, left, min_left, min_right = len(t), 0, 0, float('inf')
        memo = defaultdict(int)
        for c in t:
            memo[c] += 1
        for right, c in enumerate(s):
            if memo[c] > 0:
                missing -= 1
            memo[c] -= 1
            if missing == 0:
                while memo[s[left]] < 0:
                    memo[s[left]] += 1
                    left += 1
                if right - left < min_right - min_left:
                    min_right, min_left = right, left
                memo[s[left]] += 1
                missing += 1
                left += 1
        return '' if min_right == float('inf') else s[min_left:min_right+1]
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
- Time: O(n) -- two pointers go over once
- Space: O(1) -- memo has a fixed length