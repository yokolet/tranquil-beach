# Range Sum Query 2D - Immutable

#### Description

Given a 2D matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

The `sumRegion` (`sum_region` for Ruby) gets called multiple times. `row1 ≤ row2 and col1 ≤ col2`.

#### Example
Input:

```
matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]
```

Queries:

```
sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```

#### How to Solve

Since `sumRegion` method is called many times, its performance is important. Given that, create accumulated sum matrix in the constructor. The answer to query will be accumulated sum up to `row2, col2` - upper region - left region + doubly subtracted region.

For easiness, one extra row and col were added and initialized by zero. The indices of queries are plus one for acc sum.

#### Solution
- Python

```python
class NumMatrix:
    def __init__(self, matrix: 'List[List[int]]'):
        def sum_matrix():
            m = len(matrix)
            n = len(matrix[0]) if matrix else 0
            
            result = [[0] * (n + 1) for _ in range(m + 1)]
            for i in range(m):
                for j in range(n):
                    result[i + 1][j + 1] = result[i][j + 1] + result[i + 1][j] - result[i][j] + matrix[i][j]
            print(result)
            return result
        self.acc_sum = sum_matrix()

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        result = self.acc_sum[row2+1][col2+1]
        result -= self.acc_sum[row1][col2+1] # upper
        result -= self.acc_sum[row2+1][col1] # left
        result += self.acc_sum[row1][col1]   # adds doubly subtracted area
        return resul
```

- Ruby

```ruby
class NumMatrix

=begin
    :type matrix: Integer[][]
=end
  def initialize(matrix)
    m = matrix.size
    n = matrix[0].nil? ? 0 : matrix[0].size
    @acc_sum = [Array.new(n + 1, 0)]
    m.times do |i|
      s = matrix[i].reduce([0]) {|acc, x| acc+[acc[-1] + x]}
      @acc_sum << @acc_sum[-1].zip(s).map {|x| x[0] + x[1]}
    end
  end

=begin
    :type row1: Integer
    :type col1: Integer
    :type row2: Integer
    :type col2: Integer
    :rtype: Integer
=end
  def sum_region(row1, col1, row2, col2)
    result = @acc_sum[row2 + 1][col2 + 1]
    result -= @acc_sum[row1][col2+1]
    result -= @acc_sum[row2+1][col1]
    result += @acc_sum[row1][col1]
    result
  end
end
```

#### Complexity
- Time: creation: O(m*n) -- m is a length of row, n is a length of col, query: O(1)
- Space: O(m*n)