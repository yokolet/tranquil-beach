# Palindrome Pairs

#### Description

Given a list of unique words, find all pairs of distinct indices `(i, j)` which form a palindrome by words[i] + words[j].

#### Example 1
Input: `["abcd","dcba","lls","s","sssll"]`

Output: ` [[0,1],[1,0],[3,2],[2,4]]`

Explanation: `["dcbaabcd","abcddcba","slls","llssssll"]` are palindromes.

#### Example 2
Input: `["bat","tab","cat"]`

Output: `[[0,1],[1,0]]`

Explanation: `["battab","tabbat"]` are palindromes.

#### How to Solve

At first, create reverse word to index mapping. Since "abcd" needs "dcba" to form a palindrome, to quickly find the word exists or not, save such mappings in a dictionary (Hash in Ruby).

Next, divide a word in prefix and suffix. For example, "abcd" will be devided in ["", "abcd"], ["a", "bcd"], ["ab", "cd"], ["abc", "d"], ["abcd", ""].
If the reverse word table has a prefix as a key,  whose value (index) is not the same as the current word index, and suffix is palindrome, two word can form a palindrome.

Iterate all words of all combination of prefix and suffix.
All pairs will be found by checking the conditions above.

#### Solutions
- Python

```python
class PalindromePairs:
    def palindromePairs(self, words):
        """
        :type words: List[str]
        :rtype: List[List[int]]
        """
        result = []
        revWords = {w[::-1]: i for i, w in enumerate(words)}
        for i, word in enumerate(words):
            for j in range(len(word) + 1):
                prefix, suffix = word[:j], word[j:]
                if prefix in revWords and\
                    revWords[prefix] != i and\
                    suffix == suffix[::-1]:
                    result.append([i, revWords[prefix]])
                if j > 0 and\
                    suffix in revWords and\
                    revWords[suffix] != i and\
                    prefix == prefix[::-1]:
                    result.append([revWords[suffix], i])
        return result
```

- Ruby

```ruby
# @param {String[]} words
# @return {Integer[][]}
def palindrome_pairs(words)
  result = []
  revWords = words.each_with_index.map {|w, i| [w.reverse, i]}.to_h
  words.each_with_index do |word, i|
    (0..word.size).each do |j|
      prefix, suffix = word[0...j], word[j..-1]
      if revWords.has_key?(prefix) &&
          revWords[prefix] != i &&
          suffix == suffix.reverse
        result << [i, revWords[prefix]]
      end
      if j > 0 && revWords.has_key?(suffix) &&
          revWords[suffix] != i &&
          prefix == prefix.reverse
        result << [revWords[suffix], i]
      end
    end
  end
  result
end
```

#### Complexity
- Time: `O(n*m) `-- n is a length of a given word list, m is a length of the word in the list
- Space: `O(n)`