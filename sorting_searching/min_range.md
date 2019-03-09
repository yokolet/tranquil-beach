# Smallest Range

#### Description

Given k lists of sorted integers in ascending order, find the smallest range that includes at least one number from each of the k lists. The given list may contain duplicates. (`1 <= k <= 3500`, `-105 <= value of elements <= 105`)

- definition:
The range `[a,b]` is smaller than range `[c,d]` if `b-a < d-c` or `a < c` if `b-a == d-c`. 

#### Example
Input: `[[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]`

Output: `[20,24]`

Explanation:

Merged and sorted values and group numbers are:

```
value [0, 4, 5, 9, 10, 12, 15, 18, 20, 22, 24, 26, 30]
group [1, 0, 2, 1,  0,  1,  0,  2,  1,  2,  0,  0,  2]
```

The ranges which covers all three groups and its value differences are:
- range: [0, 4, 5], diff: 5
- range: [4, 5, 9], diff: 5
- range: [5, 9, 10], diff: 5
- range: [12, 15, 18], diff: 6
- range: [15, 18, 20], diff: 5
- range: [20, 22, 24], diff: 4

The last one has the minimum diff 4, so the answer is `[20, 24]`.

#### How to Solve

The first step is to create a sorted list.
There may be duplicated values, so each element in the sorted list has a pair of value and set of groups.

The second step is to go over the sorted list while checking missing group(s), and start index. When start index shifts, the missing group changes. Those should be reflected to the current missing groups.

#### Solution
- Python

```python
from collections import defaultdict

class MinRange:
    def smallestRange(self, nums):
        """
        :type nums: List[List[int]]
        :rtype: List[int]
        """
        all_nums = defaultdict(set)
        for i, num in enumerate(nums):
            for v in num:
                all_nums[v].add(i)
        all_nums = sorted(all_nums.items())
        min_range, min_diff = [all_nums[0][0], all_nums[-1][0]], all_nums[-1][0] - all_nums[0][0]
        start, missing, memo = 0, len(nums), defaultdict(int)
        for v, ks in all_nums:
            for k in ks:
                if k not in memo or memo[k] <= 0:
                    missing -= 1
                memo[k] += 1
            while missing <= 0 and all_nums[start][0] <= v:
                if v - all_nums[start][0] < min_diff:
                    min_range = [all_nums[start][0], v]
                    min_diff = v - all_nums[start][0]
                for k in all_nums[start][1]:
                    memo[k] -= 1
                    if memo[k] <= 0:
                        missing += 1
                start += 1
        return min_range
```

- Ruby

```ruby
# @param {Integer[][]} nums
# @return {Integer[]}
def smallest_range(nums)
  all_nums = {}
  nums.each_with_index do |num, k|
    num.each do |v|
      all_nums[v] ||= Set.new
      all_nums[v].add(k)
    end
  end
  all_nums = all_nums.sort_by { |key, val| key }
  min_range, min_diff = [all_nums[0][0], all_nums[-1][0]], all_nums[-1][0] - all_nums[0][0]
  start, missing, memo = 0, nums.size, {}
  all_nums.each do |item|
    item[1].each do |k|
      memo[k] ||= 0
      if !memo.has_key?(k) || memo[k] <= 0
        missing -=1
      end
      memo[k] += 1
    end
    while missing <= 0 && all_nums[start][0] <= item[0]
      if item[0] - all_nums[start][0] < min_diff
        min_range = [all_nums[start][0], item[0]]
        min_diff = item[0] - all_nums[start][0]
      end
      all_nums[start][1].each do |k|
        memo[k] -= 1
        if memo[k] <= 0
          missing += 1
        end
      end
      start += 1
    end
  end
  min_range
end
```

#### Complexity
- Time: `O(k * n(log(k * n)))` -- k is a number of lists, n is a number of elements in each list
- Space: `O(k * n)`