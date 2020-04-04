# Sentence Similarity 2 - Transitive

#### Description

Given two sentences, `words1` and `words2`, and a list of similar word pairs, `pairs`, find if two sentences are similar.
The `words1` and `words2` are arrays of strings.

Below are the definitions of the similarity.

- The similarity relation is transitive.

    For example, "great" and "fine" are similar, and "fine" and "good" are similar, then "great" and "good" are similar.

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
pairs = [["great", "good"], ["fine", "good"], ["acting" "drama"], ["skills","talent"]]
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

#### How to Solve

The first step is to create word groups. The words relation is transitive. The relation will be expressed by a graph or group ids by a union-find. The graph is straightforward. However, it's slow since it repeats a graph search number of given words.

The solution here uses the union-find. Instead of group ids, it uses the word itself as a group id.

Similar problems:
- [Sentence Similarity](sentence_similarity.md)

#### Solution
```python
from collections import defaultdict

class SentenceSimilarityTransitive:
    def areSentencesSimilarTwo(self, words1: 'List[str]', words2: 'List[str]', pairs: 'List[List[str]]') -> bool:
        def find(w):
            if w not in group:
                group[w] = w
                return w
            while w != group[w]:
                w = group[group[w]]
            return w
        if len(words1) != len(words2): return False
        group = {}
        for p1, p2 in pairs:
            x, y = find(p1), find(p2)
            if x != y:
                group[y] = x
        for w1, w2 in zip(words1, words2):
            if find(w1) != find(w2): return False
        return True
```

#### Complexity
- Time: `O(m+n)` -- m, n are lengths of words and pairs
- Space: `O(n)`