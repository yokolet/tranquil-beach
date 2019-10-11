# Spiral Matrix

#### Description

Given a 2D matrix of `m x n` elements (`m` rows, `n` columns), return all elements of the matrix in a spiral order.

#### Example 1
Input:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

Output: `[1,2,3,6,9,8,7,4,5]`

#### Example 2
Input:

```
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
```

Output: `[1,2,3,4,8,12,11,10,9,5,6,7]`

#### How to Solve

Keep tracking start and end index for both rows and columns. Traverse indices within those four boundaries. When a left to right traversal finishes, increment start row. When a top to bottom traversal finishes, decrement end columun. After a right to left traversal, decrement end row. After a bottom to top traversal, increment start col.

#### Solution
- Python

```python
class SpiralMatrix:
    def spiralOrder(self, matrix: 'List[List[int]]') -> 'List[int]':
        if not matrix or not matrix[0]: return []
        m, n, result = len(matrix), len(matrix[0]), []
        row_start, row_end, col_start, col_end = 0, m-1, 0, n-1
        count = m * n
        while row_start <= row_end and col_start <= col_end:
            for i in range(col_start, col_end+1):
                result.append(matrix[row_start][i])
                count -= 1
            if count == 0: break
            row_start += 1
            for i in range(row_start, row_end+1):
                result.append(matrix[i][col_end])
                count -= 1
            if count == 0: break
            col_end -= 1
            for i in range(col_end, col_start-1, -1):
                result.append(matrix[row_end][i])
                count -= 1
            if count == 0: break
            row_end -= 1
            for i in range(row_end, row_start-1, -1):
                result.append(matrix[i][col_start])
                count -= 1
            if count == 0: break
            col_start += 1
        return result
```

#### Complexity
- Time: `O(mn)` -- m,n are lengths of matrix's rows and columns
- Space: `O(1)`
