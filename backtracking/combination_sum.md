# Combination Sum

#### Description

Given an array of integers `candidates` and a taget value, find all unique combinations of candidates sum up to the target.

- Definition
    -  The integers in the candidates are unique and positive.
    - The integers from candidates may be used unlimited times.
    - The solution set must not contain duplicate combinations.

#### Example 1
Input: `candidates = [2,3,6,7]`, `target = 7`

Output:
```
[
  [7],
  [2,2,3]
]
```

#### Example 2
Input: `candidates = [2,3,5]`, `target = 8`

Output:
```
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

#### How to Solve

This problem allows to use the same integer as many times as possible. The depth first search (DFS) handles well this type of problem. If the repeated use of numbers is not allowed, dynamic programming (DP) would be a good approach.

In this solution, each combination is represented as a path.
While recursively iterating over the given array, the target decreases by the value at `candiates[idx]`. If the target becomes zero, the combination (path) is found. In each recursion, when `candiates[idx]` is less than or equal to the target, the recursion goes deeper. Once it comes back to the upper level, the index is incremented to repeat the recursion.

#### Solution
- Python

```python
class CombinationSum:
    def combinationSum(self, candidates: 'List[int]', target: int) -> 'List[List[int]]':
        def dfs(arr, target, idx, path, result):
            if target == 0:
                result.append(path)
                return
            while idx < len(arr) and arr[idx] <= target:
                dfs(arr, target-arr[idx], idx, path+[arr[idx]], result)
                idx += 1
        result = []
        dfs(sorted(candidates), target, 0, [], result)
        return result
```

- Ruby

```ruby
# @param {Integer[]} candidates
# @param {Integer} target
# @return {Integer[][]}
def combination_sum(candidates, target)
  result = []
  dfs(candidates.sort, target, 0, [], result)
  result
end
def dfs(arr, target, index, path, result)
  if target == 0
    result << path
    return
  end
  while index < arr.size && arr[index] <= target
    dfs(arr, target-arr[index], index, path+[arr[index]], result)
    index += 1
  end
end
```

#### Complexity
- Time: `O(b^m)` -- b is a branching factor, m is a max depth
- Space: `O(bm)`

In this solution b is a number of combinations, while m is a max length of combinations. In example 1, b is 2, and m is 3.
In example 2, b is 3, and m is 4.
