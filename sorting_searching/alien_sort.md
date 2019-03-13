# Verifying an Alien Dictionary

#### Description

Imagine an alien language exists that uses english lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographicaly in this alien language.

#### Example 1
nput: `words = ["hello","leetcode"]`, `order = "hlabcdefgijkmnopqrstuvwxyz"`

Output: `True`

Explanation: The 'h' comes before 'l' in this language.

#### Example 2
Input: `words = ["word","world","row"]`, `order = "worldabcefghijkmnpqstuvxyz"`

Output: False

Explanation: The 'd' comes after 'l' in this language.

#### Example 3
Input: `words = ["apple","app"]`, `order = "abcdefghijklmnopqrstuvwxyz"`

Output: False

Explanation: According to lexicographical rules `"apple" > "app"`.

#### How to Solve

For the first step, create character to index mapping.
The second step is to go through the two words from beginning.
Compare each character based on the character ot index mapping.
To handle a substring to other, this solution uses a flag, sub.
When iteration reaches to the end and the correct order continues to the one of word's end, the length of two words matters.

#### Solution
- Python

```python
class AlienSort:
    def isAlienSorted(self, words: 'List[str]', order: str) -> bool:
        memo = {}
        for i, c in enumerate(order):
            memo[c] = i
        prev = words[0]
        for cur in words[1:]:
            i, j, sub = 0, 0, True
            while i < len(prev) and j < len(cur):
                if memo[prev[i]] > memo[cur[j]]:
                    return False
                if memo[prev[i]] < memo[cur[j]]:
                    sub = False
                    break
                i += 1
                j += 1
            if len(cur) < len(prev) and sub:
                return False
            prev = cur
        return True
```

- Ruby

```ruby
# @param {String[]} words
# @param {String} order
# @return {Boolean}
def is_alien_sorted(words, order)
  memo = {}
  order.size.times { |i| memo[order[i]] = i }
  (1...words.size).each do |i|
    prev, cur, i, j, sub = words[i - 1], words[i], 0, 0, true
    while i < prev.size && j < cur.size
      if memo[prev[i]] > memo[cur[j]]
        return false
      end
      if memo[prev[i]] < memo[cur[j]]
        sub = false
        break
      end
      i += 1
      j += 1
    end
    if prev.size > cur.size && sub
      return false
    end
  end
  true
end
```

##### Complexity
- Time: `O(n*m)` -- n is a length of words list, m is a length of each words (average)
- Space: `O(1)`