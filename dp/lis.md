# Longest Increasing Subsequence

#### Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

#### Example
Input: `[10,9,2,5,3,7,101,18]`

Output: 4

Explanation: The longest increasing subsequence is `[2,3,7,101]`.

#### How to Solve

This is a so-called LIS problem. The problem asks subsequence, not subarray, so the dymanic programming approach is common.
Two pointer solution may be popular. Comparing one by one, increase the length if the condition meets. It's easy to understand, but this O(n^2) solution runs very slow. For reference, the typical two pointer solution is added in Python code.

The solution here uses a binary search. The outer loop is the same, takes each element one by one. Inner loop is the binary search. The idea is: the right index of the binary search is the current max_length. The middle value in an auxiliary array and current value in the given array will be compared.

For the example above, max_length and auxiliary array changes as in blow:

```
1 [10, 0, 0, 0,   0, 0, 0, 0]
1 [9,  0, 0, 0,   0, 0, 0, 0]
1 [2,  0, 0, 0,   0, 0, 0, 0]
2 [2,  5, 0, 0,   0, 0, 0, 0]
2 [2,  3, 0, 0,   0, 0, 0, 0]
3 [2,  3, 7, 0,   0, 0, 0, 0]
4 [2,  3, 7, 101, 0, 0, 0, 0]
```

#### Solution
- Python

```python
class LIS:
    # O(nlog(n))
    def lengthOfLIS(self, nums: 'List[int]') -> 'int':
        if not nums: return 0
        memo = [0] * len(nums)
        max_length = 0
        for i in range(len(nums)):
            left, right = 0, max_length
            while left < right:
                mid = (left + right) // 2
                if memo[mid] < nums[i]:
                    left = mid + 1
                else:
                    right  = mid
            memo[left] = nums[i]
            max_length = max(max_length, left + 1)
        return max_length


    # O(n^2) - very slow
    def lengthOfLIS_slow(self, nums: 'List[int]') -> 'int':
        if not nums: return 0
        memo = [1]*(len(nums))
        max_length = 1
        for i in range(1, len(nums)):
            j = 0
            while j < i:
                if nums[i] > nums[j] and memo[i] < memo[j] + 1:
                    memo[i] = memo[j] + 1
                    max_length = max(max_length, memo[i])
                j += 1
        return max_length
```

- Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def length_of_lis(nums)
  return 0 if nums.nil? || nums.empty?
  memo = Array.new(nums.size, 0)
  max_length = 0
  nums.each do |v|
    left, right = 0, max_length
    while left < right
      mid = (left + right) / 2
      if memo[mid] < v
        left = mid + 1
      else
        right = mid
      end
    end
    memo[left] = v
    max_length = [max_length, left + 1].max
  end
  return max_length
end
```

#### Complexity
- Time: O(nlog(n))
- Space: O(n)