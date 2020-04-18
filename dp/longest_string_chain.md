# Longest String Chain

#### Description

Given a list of words, which consists of English lowercase letters, find the longest possible length of a word chain.
The word chain is defined below:

- Definition
    - The word chain is created by the given words.
    - Each word in the word chain is a predecessor of the previous word.
    - A word1 is a predecessor of word2 if and only if adding a single letter to the word1 makes it equal to word2. For example, `"abc"` is a predecessor of `"abac"`.

#### Example

Input: `["a","b","ba","bca","bda","bdca"]`

Output: `4`

Explanation: `"a","ba","bda","bdca"` is the longest word chain.

#### How to Solve

A word length based dictionary and dynamic programmin (DP) is one of possible solutions. Once The word length dictionary is created, start from longest to shortest. The search repeats: 1. find predecessor words, 2. update the chain length, 3. check max chain length.

#### Solution
- Python

```python
from collections import defaultdict

class LongestStringChain:
    def longestStrChain(self, words: 'List[str]') -> int:
        def findPred(a):
            preds = set()
            for i in range(len(a)):
                tmp = a[:i]+a[i+1:]
                if tmp not in preds and tmp in w_dict[len(a)-1]:
                    preds.add(tmp)
            return preds
        
        w_dict = defaultdict(set)
        for w in words:
            w_dict[len(w)].add(w)
        max_len, memo = 1, defaultdict(lambda:1)
        for l in range(16, 1, -1):    # 1 <= words[i] <=16
            if l not in w_dict or l-1 not in w_dict: continue
            for w in w_dict[l]:
                preds = findPred(w)
                for p in preds:
                    memo[p] = max(memo[p], memo[w]+1)
                    max_len = max(max_len, memo[p])
        return max_len
```

#### Complexity
- Time: `O(n)` -- n is a length of given word list
- Space: `O(mp)` -- m, p are numbers of words in the specific length group and predecessors respectively.
