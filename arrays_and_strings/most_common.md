# Most Common Word

#### Description

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.

It is guaranteed there is at least one word that isn't banned, and that the answer is unique. Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

#### Example
Input: 
paragraph = `"Bob hit a ball, the hit BALL flew far after it was hit."`
banned = `["hit"]`

Output: `"ball"`

Explanation: 
"hit" occurs 3 times, but it is a banned word. "ball" occurs twice and is not listed in banned.

#### How to Solve

Split the given paragraph into words which only include word characters. Count frequencies of words which is not listed in banned.

#### Solution
- Python

```python
import re
from collections import Counter

class MostCommon:
    def mostCommonWord(self, paragraph: str, banned: 'List[str]') -> str:
        words = re.findall(r'\w+', paragraph.lower())
        return Counter(w for w in words if w not in banned).most_common(1)[0][0]
```

- Ruby

```ruby
# @param {String} paragraph
# @param {String[]} banned
# @return {String}
def most_common_word(paragraph, banned)
  memo = Hash.new { |h, k| h[k] = 0 }
  max_count = 0
  result = nil
  paragraph.downcase.scan(/\w+/).each do |word|
    memo[word] += 1 if !banned.include?(word)
    if max_count < memo[word]
      max_count = memo[word]
      result = word
    end
  end
  result
end
```

#### Complexity
- Time: O(n+m) -- n is a length of words in paragraph, m is a length of banned
- Space: O(n)