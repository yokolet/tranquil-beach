# Compare Strings by Frequency of the Smallest Character

#### Description

Given two arrays of strings, `queries` and `words`, find how many words in `words` satisfy the conditions below against each query word in `queries`.

- Definition
    - Function: calculates the frequency of the smallest character in `s` over a non-empty string `s`.
    - Comparison: only when `f(query) < f(word)`, the word should be counted as a result of the query.

#### Example 1
Input: `queries = ["cbd"], words = ["zaaaz"]`

Output: `[1]`

Explanation: `f("cbd")=1` since `c` is the smallest and its frequency is 1. `f("zaaaz")=3` since `a` is the smallest and its frequency is 3. The query satisfies the conidition, `f("cbd") < f("zaaaz")`, so the answer is `[1]`.

#### Example 2
Input: `queries = ["bbb","cc"], words = ["a","aa","aaa","aaaa"]`

Output: `[1,2]`

Explanation: After applying the function, `queries = [3,2]`, `words = [1,2,3,4]`. For the query one, the last word satisfies the condition. For the query 2, the last two words satisfies the condition.

#### How to Solve

The function should be implemented first. This solution uses Python's string functions which are simple and effective. It may happen the function returns the same value for multiple words in `words` list. For this reason, a frquency to word count pairs are saved in the dictionary. To use in the queries, the keys are sorted in ascending order and saved in the array. The last piece is to iterate over the query words. The word frequency is sorted in an ascending order, so check from the last to first element. Sum up the word count while word frequency is greater than query's frequency.

#### Solution
- Python

```python
from collections import defaultdict

class SmallestCharacter:
    def numSmallerByFrequency(self, queries: 'List[str]', words: 'List[str]') -> 'List[int]':
        def counter(w):
            return w.count(min(w))
        w_freq = defaultdict(int)
        for w in words:
            w_freq[counter(w)] += 1
        w_values = sorted(w_freq.keys(), reverse=True)
        result = []
        for q in queries:
            q_freq = counter(q)
            cnt = 0
            for w_val in w_values:
                if w_val > q_freq: cnt += w_freq[w_val]
                else: break
            result.append(cnt)
        return result
```

#### Complexity
- Time: `O(m*n)` -- m, n are the length of each word and word/query list respectively.
- Space: `O(n)`
