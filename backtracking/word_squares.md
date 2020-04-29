# Word Squares

#### Description

Given a set of unique words, find all word squares built from the given words. All words are exactly the same length and contains only lowercase English letters a-z. The definition of word square is below:

- Definition
    - if the word length is n, the squares will have the size of n x n.
    - k-th row and k-th column are the exact same strings. 

#### Example 1

Input: `["area","lead","wall","lady","ball"]`

Output: (the order of the two squares doesn't matter)

```
[
  [ "wall",
    "area",
    "lead",
    "lady"
  ],
  [ "ball",
    "area",
    "lead",
    "lady"
  ]
]
```

#### Example 2

Input: `["abat","baba","atan","atal"]`

Output: (the order of the two squares doesn't matter)

```
[
  [ "baba",
    "abat",
    "baba",
    "atan"
  ],
  [ "baba",
    "abat",
    "baba",
    "atal"
  ]
]
```

#### How to Solve

The backtracking works well for this problem.
The basic idea is to extend a prefix one by one while checking the prefix exists. When the prefix goes longer, it goes to deeper stack of bactracking. If the prefix length becomes one of the word itself, a square is found.

To solve this problem, the prefix mapping is the key. The prefix mappings are:

```
# the first example
{
    'a': {'area'},
    'ar': {'area'},
    'are': {'area'},
    'l': {'lead', 'lady'},
    'le': {'lead'},
    'lea': {'lead'},
    'w': {'wall'},
    'wa': {'wall'},
    'wal': {'wall'},
    'la': {'lady'},
    'lad': {'lady'},
    'b': {'ball'},
    'ba': {'ball'},
    'bal': {'ball'}
}
```

Suppose the word `ball` is in the array in the backtracking method. The second word candidate is `area` only since the prefix is `a`. The previous word is `area`, so the prefix should be `le` concatenating the index 2 of `ba[l]l` and `ar[e]a`. The next prefix should be `lad` concatenating the index 3 of `bal[l]`, `are[a]` and `lea[d]`.

When it comes from the deeper backtraking stack, pop the last word for the next word in the same level.

#### Solution
- Python

```python
from collections import defaultdict

class WordSquares:
    def wordSquares(self, words: 'List[str]') -> 'List[List[str]]':
        def prefixMap():
            d = defaultdict(set)
            for w in words:
                for p in [w[:i] for i in range(1, n)]:
                    d[p].add(w)
            return d

        def backtrack(idx, sub):
            if idx == n:
                result.append(sub[:])
                return
            prefix = ''.join([w[idx] for w in sub])
            if prefix not in prefix_dict: return
            for w in prefix_dict[prefix]:
                sub.append(w)
                backtrack(idx+1, sub)
                sub.pop()
        
        n = len(words[0])
        prefix_dict = prefixMap()
        result = []
        for w in words:
            backtrack(1, [w])
        return result
```

#### Complexity
- Time: `O(n*26^l)` -- n, l are a number of given words and length of each word repectively
- Space: `O(nl)`
