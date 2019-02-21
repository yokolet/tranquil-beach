# Letter Combinations of a Phone Number

#### Description

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. The '1' does not map to any letters.

```
1       2 abc   3 def
4 ghi   5 jkl   6 mno
7 pqrs  8 tuv   9 wxyz
*       0 +     #
```

#### Example

Input: `23`

Output: `["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]`

#### How to Solve

This is a combination problem. The logic is not complicated.
Taking a letter one by one, it creates all letter combinations.
DFS may be a good approach.

Instead of using DFS, the solution here is a loop of array manipulation. Not all languages have this sort of feature.
Python solution is a succinct one liner.
Ruby uses a combination of reduce and map, but is still a one liner and equivalent to Python.

#### Solution

{% code-tabs %}

{% code-tabs-item title=Python %}
```python
class LetterCombinations:
     def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if not digits: return []   
        letters = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }
        n = len(digits)
        result = list(letters[digits[0]])
        if n == 1:
            return result
        idx = 1
        while idx < n:
            result = [x + y for x in result for y in letters[digits[idx]]]
            idx += 1
        return result
```
{% endcode-tabs-item %}

{% code-tabs-item title=Ruby %}
```ruby
  # @param {String} digits
  # @return {String[]}
  def letter_combinations(digits)
    return [] if digits.nil? || digits.empty?
    letters = {
        '2' => ['a', 'b', 'c'],
        '3' => ['d', 'e', 'f'],
        '4' => ['g', 'h', 'i'],
        '5' => ['j', 'k', 'l'],
        '6' => ['m', 'n', 'o'],
        '7' => ['p', 'q', 'r', 's'],
        '8' => ['t', 'u', 'v'],
        '9' => ['w', 'x', 'y', 'z']
    }
    n = digits.size
    result = letters[digits[0]]
    return result if n == 1
    (1...n).each do |idx|
      result = result.reduce([]) {|acc, s| acc + letters[digits[idx]].map {|l| s + l}}
    end
    result
  end
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Complexity
- Time O(k^n) : k is 3 or 4, n is a length of given digits
- Space O(k^n) : result array ends up growing to k^n
