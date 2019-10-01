# Rotate Image

#### Description

Given an `n x n` 2-d matrix which represents an image, rotate the image 90 degrees clockwise.

The rotation must be done in-place. Do not create a new matrix.

#### Example 1
Input:

```
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
]
```

After rotation:

```
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

#### Example 2
Input:

```
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
]
```

After rotation:

```
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

#### How to Solve

There are a couple of approaches to solve this problem.
The easiest would be to reverse rows, then swap values along the diagonal line. For example, `(0,1)<->(1,0), (1,2)<->(2,1)`.

#### Solution
- Python

```python
class RotateImage:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        matrix.reverse()
        for i in range(len(matrix)):
            for j in range(i):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
```

#### Complexity
- Time: `O(n^2)` -- n is a length of rows or columns
- Space: `O(1)`
