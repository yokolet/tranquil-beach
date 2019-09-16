# Monotonic Array

#### Description

Given and array of integers, return true if the array is monotonic. Othereise, return false.

- Definition

    An array is monotonic if it is either monotone increasing or monotone decreasing.

    An array A is monotone increasing if for all `i <= j`, `A[i] <= A[j]`.  An array A is monotone decreasing if for all `i <= j`, `A[i] >= A[j]`.

#### Example 1
Input: `[1,2,2,3]`

Output: `True`

#### Example 2
Input: `[6,5,4,4]`

Output: `True`

#### Example 3
Input: `[1,3,2]`

Output: `False`

#### Example 4
Input: `[1,2,4,5]`

Output: `True`

#### Example 5
Input: `[1,1,1]`

Output: `True`

#### How to Solve

If the first and last element are compared, it's clear the array is whether monotone increaseing (non-increasing) or decreasing.
Compare each element with the previous one and check it is monotonically increaseing, or decreasing.

#### Solution
- Python

```python
class Monotonic:
    def isMonotonic(self, A: 'List[int]') -> bool:
        factor = 1 if A[0] <= A[-1] else -1
        prev = A[0]
        for cur in A[1:]:
            if (cur - prev)*factor < 0:
                return False
            prev = cur
        return True
```

- Ruby

```ruby
# @param {Integer[]} a
# @return {Boolean}
def is_monotonic(a)
  factor = a[0] <= a[-1] ? 1 : -1
  prev = a[0]
  a.each do |x|
    return false if (x - prev) * factor < 0
    prev = x
  end
  true
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(1)`
