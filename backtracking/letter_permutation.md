# Letter Case Permutation

#### Description

Given a string `S`, find all possible strings when each letter is changed to lowercase or uppercase.

#### Example 1
Input: `S = "a1b2"`

Output: `["a1b2", "a1B2", "A1b2", "A1B2"]`

#### Example 2
Input: `S = "3z4"`

Output: `["3z4", "3Z4"]`

#### Example 3
Input: `S = "12345"`

Output: `["12345"]`

#### How to Solve

The approach is taking a character one by one to create all possible combinations. The solution here uses a loop of array manipulation. At first, it creates a list of possible characters. Then, starting from empty string, each character is added to previously created strings in the list.

#### Solution
- Python

```python
class LetterPermutation:
    def letterCasePermutation(self, S: str) -> 'List[str]':
        s = [[c.lower(), c.upper()] if c.isalpha() else c for c in S]
        result = ['']
        for i in range(len(S)):
            result = [x + y for x in result for y in s[i]]
        return result
```

#### Complaxity
- Time: `O(2^n)` -- n is a length of the given string
- Space: `O(2^n)`
