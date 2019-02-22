# Combination Sum

#### Description

Given an array of integers (candidates) and a taget value, find all unique combinations of candidates sum up to the target.

The integers in the candidates are unique and positive.
The integers from candidates may be used unlimited times.
The solution set must not contain duplicate combinations.

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

In this solution, each combination is represented as path.
While going deeper, the target value decreases by candiates[index]. In each stack, candiates[index] is less than or equal to decreased target value, it goes deeper. Unless, it comes back and choose next value in the candiates.

When decreased target value becomes 0, the path is one of the result combination.

#### Solution
- Python

```python
class CombinationSum:
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        def dfs(arr, target, index, path, result):
            if target == 0:
                result.append(path)
                return
            while index < len(arr) and arr[index] <= target:
                dfs(arr, target-arr[index], index, path+[arr[index]], result)
                index += 1
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
- Time: O(b^m) -- b is a branching factor, m is a max depth
- Space: O(bm)

In this solution b is a number of combinations, while m is a max length of combinations. In example 1, b is 2, and m is 3.
In example 2, b is 3, and m is 4.
