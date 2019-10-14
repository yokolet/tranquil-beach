# Implement Trie (Prefix Tree)

#### Description

Implement a trie data strucutre with `insert`, `search` and `startWith` methods.

#### Example
```python
trie = Trie()

trie.insert('apple')
trie.search('apple')    # returns True
trie.search('app')      # returns False
trie.startsWith('app')  # returns True
trie.insert('app')
trie.search('app')      # returns True
```

#### How to Solve

The trie data structure has a shape of tree. Each node in tree is a dictionary whose key is a single character and value is a dictionary (child nodes). Both insert and search operations traverse the tree vertically. How to mark the end of the word should be considered. The solution here simply adds an end marker in the tree. Another possible way is to define a node class which has the word end property.

#### Solution
- Python

```python
class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.children = {}
        self.marker = '$'

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        cur = self.children
        for c in word:
            if c not in cur:
                cur[c] = {}
            cur = cur[c]
        cur[self.marker] = None

    def __search__(self, word: str) -> bool:
        cur = self.children
        for c in word:
            if c not in cur: return False
            cur = cur[c]
        return True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        return self.__search__(word + self.marker)

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        return self.__search__(prefix)
```

#### Complexity
- Time: `O(m)` -- m is a lenght of an insert or search word.
- Space: `O(mn)` -- n is a totla number of words
