# Sentence Similarity

#### Description

Given two sentences, `words1` and `words2`, and a list of similar word pairs, `pairs`, find if two sentences are similar.
The `words1` and `words2` are arrays of strings.

Below are the definitions of the similarity.

- The similarity relation is not transitive.

    For example, "great" and "fine" are similar, and "fine" and "good" are similar, but "great" and "good" are NOT necessarily similar.

- The similarity is symmetric.

    For example, if "great" and "fine" are similar, "find" and "good" are similar.

- A word is alywas similar with itself.

    For example, the word "great" in the `words1` array and the "great" in the `words2` array at the same index are similar even though the pairs list is empty.

- Sencences can be similar only if number of words are the same.

#### Example 1

Input:
```
words1 = ["great", "acting", "skills"]
words2 = ["fine", "drama", "talent"]
pairs = [["great", "fine"], ["acting","drama"], ["skills","talent"]]
```

Output: `True`

#### Example 2

Input:
```
words1 = ["great"]
words2 = ["great"]
pairs = []
```

Output: `True`

#### Example 3

Input:
```
words1 = ["an","extraordinary","meal"]
words2 = ["one","good","dinner"]
pairs = [["extraordinary","good"],["well","good"],["wonderful","good"],["any","one"],["an","one"],["a","one"],["food","meal"],["dinner","meal"],["lunch","meal"]]
```

Output: `True`

#### How to Solve

The first step is to create a word relation map. The relation is symmetric, so both directions should be added. The relation is not one-to-one only. So, the set is used to save each relation from one word to multiple words.

After the word map is created, each word pair in `words1` and `words2` are compaired.

Similar problems:
- [Sentence Similarity 2 - Transitive](sentence_similarity_transitive.md)

#### Solution

```python
from collections import defaultdict

class SentenceSimilarity:
    def areSentencesSimilar(self, words1: 'List[str]', words2: 'List[str]', pairs: 'List[List[str]]') -> bool:
        if len(words1) != len(words2): return False
        p_dict = defaultdict(set)
        for p1, p2 in pairs:
            p_dict[p1].add(p2)
            p_dict[p2].add(p1)
        for i in range(len(words1)):
            if words1[i] == words2[i] or\
                (words1[i] in p_dict and words2[i] in p_dict[words1[i]]):
                continue
            return False
        return True
```

#### Complexity
- Time: `O(m+n)` -- m, n are lengths of words and pairs
- Space: `O(n)`
