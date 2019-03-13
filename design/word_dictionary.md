# Add and Search Word - Data structure design

#### Description

Design a data structure that supports the following two operations:

```
void addWord(word)
bool search(word)
```

The method, search(word), can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter. All words are consist of lowercase letters a-z.

#### Example

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

#### How to Solve

Use dictionary (Hash for Ruby) to save words given by `addWord` method. The key is word length and value is a set of words.
This design is to search a word quickly. Especially, the answer "doesn't exist" runs in a constant time. Also, exact match runs still in a constant time.

When a given search word includes ".", it needs to check all words in the same length, possibly narrowing down next words to be checked. In any case, all characters of all words need to be checked.

#### Solution
- Python

```python
from collections import defaultdict

class WordDictionary:

    def __init__(self):
        """
        Instantiate WordDictionary
        """
        self.table = defaultdict(set) # {word_length: set of words}

    def addWord(self, word):
        """
        Adds a word into the data structure.
        :type word: str
        :rtype: void
        """
        self.table[len(word)].add(word)

    def search(self, word):
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        :type word: str
        :rtype: bool
        """
        length = len(word)
        if length not in self.table: return False
        if word in self.table[length]: return True
        tmp = self.table[length]
        for i in range(length):
            if word[i] == '.':
                continue
            tmp = {c for c in tmp if c[i] == word[i]}
            if not tmp: return False
        return True
```

- Ruby

```ruby
require 'set'

class WordDictionary
  # Instantiate WordDictionary
  def initialize()
    @table = Hash.new { |h, k| h[k] = Set.new } # {word_length => set of words}
  end

  # Adds a word into the data structure
  # @param [String] word
  # @return nil
  def add_word(word)
    @table[word.size].add(word)
    nil
  end

  # Returns true if the word is in the data structure.
  # A word could contain the dot character '.' to represent any one letter.
  #
  # @param [String] word
  # @return [true] if exists, false it not
  def search(word)
    length = word.size
    return false if !@table.has_key?(length)
    return true if @table[length].include?(word)
    tmp = @table[length]
    length.times do |i|
      next if word[i] == "."
      tmp = tmp.reduce([]) {|acc, e| acc << e if e[i] == word[i]; acc }
      return false if tmp.empty?
    end
    true
  end
end
```

#### Complexity
- Time: addWord: O(1), search: O(n*m) -- n is length of the set, m is average length of words
- Space: O(l) -- l is number of lengths of added words