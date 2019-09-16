# Reorder Log Files

#### Description

Given an array of logs, reorder the the logs following the rules below:

- Each log is a space delimited string of words.
- The first word in each log is an alphanumeric identifier.
- Each word after the identifier will consist only of lowercase letters.
- Or, each word after the identifier will consist only of digits.
- In the final order of the logs, the letter-logs come before any digit-log.
- In the final order of the logs, the letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties.
- In the final order of the logs, the digit-logs should be put in their original order.

logs[i] is guaranteed to have an identifier, and a word after the identifier.

#### Example
Input: `["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]`

Output: `["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]`

#### How to Solve

Custom sort was used for this solution. The sort is performed comparing (0, letters after id, id) and (1). Both Python and Ruby's sort works to meet with this problem's requirement.

#### Solution
- Python

```python
class ReorderLog:
    def reorderLogFiles(self, logs: 'List[str]') -> 'List[str]':
        def key_f(log):
            id_, rest = log.split(' ', 1)
            if rest[0].isdigit():
                return (1,)
            else:
                return (0, rest, id_)
        return sorted(logs, key=key_f)
```

- Ruby

```ruby
# @param {String[]} logs
# @return {String[]}
def reorder_log_files(logs)
  logs.sort_by do |log|
    id_, *rest = log.split(/\s/)
    rest[0].match(/\D/) ? [0, rest, id_] : [1]
  end
end
```

#### Complexity
- Time: `O(nlog(n))`
- Space: `O(1)`
