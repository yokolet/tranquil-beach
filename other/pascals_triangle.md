# Pascal's Triangle

#### Description

Given a non-negative integer `numRows`, generate the first `numRows` of Pascal's triangle.

- Definition

    Pascal's triangle is a triangular array of the binomial coefficients.

#### Example
Input: `5`

Output:

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

#### How to Solve

Let `C(line, i)` be the binominal coefficient at `i`-th entry in `line`.

```
C(line, i) = line! / ((line - 1)! * i!)
C(line, i-1) = line! / ((line - i + 1)! * (i-1)!)
from above two
C(line, i) = C(line, i-1)* (line - i +1 ) / i
```

Starting from `C=1`, repeat the last formula until the line becomes `numRows`.

#### Solution
- Python

```python
class PascalsTriangle:
    def generate(self, numRows: int) -> 'List[List[int]]':
        result = []
        for line in range(1, numRows+1):
            C = 1
            sub = []
            for i in range(1, line+1):
                sub.append(C)
                C = int(C * (line - i) / i)
            result.append(sub)
        return result
```

#### Complexity
- Time: `O(n^2)` -- n is a number of rows
- Space: `O(1)` -- except the result array, it is constant
