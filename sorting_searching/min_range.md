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

The solution uses heap as a data structure to save the combination of (v, i, j), where v is a value at i-th nums of j-th index. Starting from one combination from all nums, the solution takes smallest value from the heap one by one. Each time, the mininum range is compared. Then, a value of the next index of the same i-th nums is added to heap. Also, maximum value is updated. When one of the nums comes to the end, the minimum range will be returned. This is because, there'a no more range to cover all nums.

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
        queue = [(nums[i][0], i, 0) for i in range(len(nums))]
        heapq.heapify(queue)
        max_v = max(queue)[0]
        min_range = [float('-inf'), float('inf')]
        while queue:
            min_v, i, j = heapq.heappop(queue)
            if max_v - min_v < min_range[1] - min_range[0]:
                min_range = [min_v, max_v]
            if j == len(nums[i])-1:
                return min_range
            v = nums[i][j + 1]
            max_v = max(max_v, v)
            heapq.heappush(queue, (v, i, j + 1))
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
- Python
    - Time: `O((k+n)log(k+n))` -- -- k is a number of lists, n is a number of elements in each list
    - Space: `O(k)`
- Ruby
    - Time: `O(k * n(log(k * n)))`
    - Space: `O(k * n)`