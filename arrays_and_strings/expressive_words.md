# Expressive Words

#### Description

Given a string `S` and query words, count stretchy words in the query.

- Definition

    A query word is stretchy if it can create the string `S` by adding the same character more than 2 in each character group or adding nothing.

#### Example
Input: `S="heeellooo", words = ["hello", "hi", "helo"]`

Output: `1`

Explanation:

"hello" is a stretchy since `"hello" -> "h", "e", "ll", "o" -> "h", "eee", "ll", "ooo"`.

"hi" is not a stretchy since it doesn't have all characters to create `S`.

"helo" is not a strechy since `"helo" -> "h", "e", "l", "o" -> "h", "eee", "l" or "lll", "ooo"`.

#### How to Solve

For the first step, word's character groups and those counts should be calculated. If a query word has the same characters and length of groups, check individual counts. Suppose each counts in `S` and `word` in `words` are `cnt` and `w_cnt` respectively, these should be `cnt == w_cnt` or `cnt >= max(w_cnt, 3)`. If all groups satisfies the conidition, count up.

#### Solution
- Python

```python
class ExpressiveWords:
    def expressiveWords(self, S: str, words: 'List[str]') -> int:
        def findGroup(w):
            prev, chars, counts = '', [], []
            for i in range(len(w)):
                if prev == w[i]:
                    counts[-1] += 1
                else:
                    chars.append(w[i])
                    counts.append(1)
                prev = w[i]
            return chars, counts
        
        chars, counts = findGroup(S)
        result = 0
        for w in words:
            w_chars, w_counts = findGroup(w)
            if chars != w_chars: continue
            result += all(cnt >= max(w_cnt, 3) or cnt == w_cnt
                       for cnt, w_cnt in zip(counts, w_counts))
        return result
```

#### Complexity
- Time: `O(mn)` - m,n are length of word and word list respectively
- Space: `O(g)` - g is a number of character groups