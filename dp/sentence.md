# Sentence Screen Fitting

#### Description

Given rows and cols of a screen and a list of non-empty words which represents a sentence, find how many times the given sentence can be fitted on the screen.

- Definitions
    - A word cannot be split in to two lines.
    - The order of words in the list must be remain unchanged.
    - Two consecutive words must be separated by a single spce in a line.

#### Example 1
Input: `rows = 2, cols = 8, sentence = ['hello', 'world']`

Output: `1`

Explanation:

```
  1 2 3 4 5 6 7 8
1 h e l l o - - -
2 w o r l d - - -
```

`-` represents a space

#### Example 2
Input: `rows = 3, cols = 6, sentence = ['a', 'bcd', 'e']`

Output: `2`

Explanation:

```
  1 2 3 4 5 6
1 a - b c d -
2 e - a - - -
3 b c d - e -
```

#### Example 3
Input: `rows = 4, cols = 5, sentence = ['I', 'had', 'apple', 'pie']`

Output: `1`

Explanation:

```
  1 2 3 4 5
1 I - h a d
2 a p p l e
3 p i e - I
4 h a d - -
```

#### How to Solve

There would be many approaches to solve this problem. The solution here took a DP approach. Before counting the characters to fit in, it creates a list which expreses how may spaces are need to fit the word. The list is created from a space concatenated words (a sentence). While iterating the sentence, if the space is found, set the start of the word to that index. Otherwise, keep incrementing the length. Once the list is created, count how many words can fit in the single row. If the list is looked up at the sentence length so far, it's clear the word length to go next row.
In the end, add one since the row count starts from zero. Then divide by the sentence length.

#### Solution
- Python

```python
class Sentence:
    def wordsTyping(self, sentence: 'List[str]', rows: int, cols: int) -> int:
        words = ' '.join(sentence) + ' '
        start, n = -1, len(words)
        memo = [0 for _ in range(n)]
        for i in range(n):
            if words[i] == ' ':
                start = i
            memo[i] = i - start - 1
        
        length = 0
        for _ in range(rows):
            length += cols
            length -= memo[length % n]
        return (length + 1) // n
```

#### Complexity
- Time: `O(m+n)` -- m, n are the lengths of a sentence and rows respectively.
- Space: `O(n)`
