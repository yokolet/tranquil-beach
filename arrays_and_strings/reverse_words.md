# Reverse Words in a String

#### Description

Given a string, reverse the string word by word.

#### Example 1

Input: `"the sky is blue"`

Output: `"blue is sky the"`

#### Example 2

Input: `"  hello world!  "`

Output: `"world! hello"`

#### Example 3

Input: `"a good   example"`

Output: `"example good a"`

#### How to Solve

Split the string to make a word list, then reverse words.
Python's `split()`(empty arg) method cuts spaces out, so words only are in the list.

#### Solution

- Python

```python
class ReverseWords:
    def reverseWords(self, s: str) -> str:
        return ' '.join(s.split()[::-1])
```

#### Complexity

- Time: `O(n)` -- n is a number of words after the string split
- Space: `O(n)`