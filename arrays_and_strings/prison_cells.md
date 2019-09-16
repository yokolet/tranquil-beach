# Prison Cells After N Days

#### Description

Given an array of 8 elements, compute the state of N updates following the rule below.

- Each element has an initial state occupied (1), or vacant(0)
- Each element interacts with its both sides
- If a cell has two adjacent neighbors that are both occupied or both vacant, then the cell becomes occupied (1).
- Otherwise, it becomes vacant (0).

N's range: `1 <= N <= 10^9`

#### Example 1
Input: `cells = [0,1,0,1,1,0,0,1], N = 7`

Output: `[0,0,1,1,0,0,0,0]`

Explanation: cells transition of 7 days:

```
Day 0: [0, 1, 0, 1, 1, 0, 0, 1]
Day 1: [0, 1, 1, 0, 0, 0, 0, 0]
Day 2: [0, 0, 0, 0, 1, 1, 1, 0]
Day 3: [0, 1, 1, 0, 0, 1, 0, 0]
Day 4: [0, 0, 0, 0, 0, 1, 0, 0]
Day 5: [0, 1, 1, 1, 0, 1, 0, 0]
Day 6: [0, 0, 1, 0, 1, 1, 0, 0]
Day 7: [0, 0, 1, 1, 0, 0, 0, 0]
```

#### Example 2
Input: `cells = [1,0,0,1,0,0,1,0], N = 1000000000`

Output: `[0,0,1,1,1,1,1,0]`

#### How to Solve

All possible combinations of 8 cells are at most `2^8 = 256`.
No matter how big the N is, the patterns of cells are limited.
Given that, save the pattern already computed with the N. If the same patterns appears, update N and save the pattern and N pair.
Compute the next cell pattern.

#### Solution
- Python

```python
class PrisonCells:
    def prisonAfterNDays(self, cells: 'List[int]', N: int) -> 'List[int]':
        patterns = {}
        while N > 0:
            c = tuple(cells)
            if c in patterns:
                N %= (patterns[c] - N)
            patterns[c] = N
            if N >= 1:
                N -= 1
                cells = [0] + [cells[i-1] ^ cells[i+1] ^ 1 for i in range(1, 7)] + [0]
        return cells
```

- Ruby

```ruby
# @param {Integer[]} cells
# @param {Integer} n
# @return {Integer[]}
def prison_after_n_days(cells, n)
  patterns = {}
  while n > 0
    if patterns.has_key?(cells)
      n %= (patterns[cells] - n)
    end
    patterns[cells] = n
    if n >= 1
      n -= 1
      cells = (0..7).map do |i|
        next 0 if i == 0 || i == 7
        cells[i-1] ^ cells[i + 1] ^ 1
      end
    end
  end
  cells
end
```

#### Complexity
- Time: `O(1)` -- O(2^8) which is constant, so O(1)
- Spaces: `O(1)` -- O((2^8)*8), which is constant, so O(1)
