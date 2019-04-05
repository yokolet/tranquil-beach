# Word Ladder - Length

#### Description

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord. Return 0 if there is no transformation sequence.

- Definition
    - Only one letter can be changed at a time.
    - Each transformed word must exist in the word list.
    - The beginWord is not a transformed word.
    - All words have the same length.
    - All words contain only lowercase alphabetic characters.
    - There's no duplicate in the word list.
    - Both beginWord and endWord are non-empty and are not the same.

#### Example 1
Input:

```
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]
```

Output: `5`

Explanation: One of the shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`

#### Example 2
Input:

```
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]
```

Output: `0`

Explanation: The endWord "cog" is not in wordList.

#### How to Solve

The breadth first search is the approach this solution takes. Start from the beginWord and change one character by a-z, check the word is in the wordList. For example, the beginWord is "hit", test
ait, bit, , , ,hat, hbt, , ,hia, hib, , , , hiz. If the tranformed word is in the list, add it to the next layer word list. When it goes to the next layer, increment the level which starts from 1.

The solution here is attempting a bidirectional search to quickly reach to the result. Creates begin_set and end_set at the beginning, swap these two so that always begin_set  length becomes less. This way, the solution cuts down the iterations.

#### Solution
- Python

```python
class LadderLength:
    def ladderLength(self, beginWord: str, endWord: str, wordList: 'List[str]') -> int:
        if endWord not in wordList: return 0
        n, visited, wordSet = len(beginWord), set(), set(wordList)
        begin_set, end_set = {beginWord}, {endWord}
        level = 1 # begin word
        while begin_set and end_set:
            level += 1
            nextLayer = set()
            for word in begin_set:
                for i in range(n):
                    prefix, suffix = word[:i], word[i+1:]
                    for c in "abcdefghijklmnopqrstuvwxyz":
                        nextWord = prefix + c + suffix
                        if nextWord in end_set: return level
                        if nextWord in wordSet and nextWord not in visited:
                            visited.add(nextWord)
                            nextLayer.add(nextWord)
            begin_set = nextLayer
            if len(begin_set) > len(end_set):
                begin_set, end_set = end_set, begin_set
        return 0
```

- Ruby

```ruby
# @param {String} begin_word
# @param {String} end_word
# @param {String[]} word_list
# @return {Integer}
def ladder_length(begin_word, end_word, word_list)
  return 0 if !word_list.include?(end_word)
  n, visited, word_set = begin_word.size, Set.new, Set.new(word_list)
  begin_set, end_set = Set[begin_word], Set[end_word]
  letters = ("a".."z").to_a
  level = 1 # begin word
  while !begin_set.empty? && !end_set.empty?
    level += 1
    nextLayer = Set.new
    begin_set.each do |word|
      n.times do |i|
        prefix, suffix = word[0, i], word[i+1, n-i]
        letters.each do |c|
          next_word = prefix + c + suffix
          return level if end_set.include?(next_word)
          if word_set.include?(next_word) && !visited.include?(next_word)
            visited.add(next_word)
            nextLayer.add(next_word)
          end
        end
      end
    end
    begin_set = nextLayer
    if begin_set.size > end_set.size
      begin_set, end_set = end_set, begin_set
    end
  end
  0
end
```

#### Complexity
- Time:
- Space: