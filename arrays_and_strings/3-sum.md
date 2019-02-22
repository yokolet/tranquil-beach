# 3 Sum

#### Description

Given an array `nums` of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

The solution set must not contain duplicate triplets.

#### Example
Input: `nums = [-1, 0, 1, 2, -1, -4]`

Output: `[[-1, 0, 1], [-1, -1, 2]]`

#### How to Solve

Typical solution is to use three pointers.  After sorting the array,
it takes the first and second values from the smallest and find
the third value. A binary search is used to find the third one.
However, this approach is not fast since O(n^2) times of
binary searchs are made.

The solution here focuses on the target value is zero.
If the target value is random, this solution doesn't work.

The first step is to count what values appear how many times and
save it to a dictionary (Hash, or Map).
The second step is to make two groupes by positive or negative.
The combination of three values should sum up to zero, so two values
are taken one from positive group and another from negative group.

Let those values to be `a <= 0`, `b > 0`. The third value is:

```
a + b + c = 0
c = -(a + b)
```

If `c` is a key of the dictionary, check the count of that value.
This is because `c` may be the same value as `a` or `b`. 
If the count value is greater than 1, the combination is one of the
result. This way, `c` will be found.
Edge case is `[0, 0, 0]`. Zeros only exist in the negative group.
But, `[0, 0, 0]` should be included in the result. So, the code
checks the count of `0`.

As an additional note, be careful, Python's collections.Counter runs slow. Simply iterating over the array is much faster.

The time complexity of this solution is O(n^2). Selecting values from positive and negative groups gives the worst performance.
When given values are divided in two groups evenly, the performace is the worst.

#### Solution

```python
def threeSum(nums):
    """
    :type nums: List[int]
    :rtype: List[List[int]]
    """
    memo = defaultdict(int)
    for v in nums:
        memo[v] += 1
    pos = []
    neg = []
    for key in memo:
        if key > 0:
            pos.append(key)
        else:
            neg.append(key)
    pos.sort()
    neg.sort()
    result = []
    if 0 in memo and memo[0] >= 3:
        result.append([0, 0, 0])
    for a in neg:
        for b in pos:
            c = -(a + b)
            if c not in memo:
                continue
            if c > b:
                result.append([a, b, c])
            elif c < a:
                result.append([c, a, b])
            elif c in (a, b) and memo[c] > 1:
                # c is the same as a or b
                # c should present more than 1 in nums
                result.append([a, c, b])
    return result
```

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def three_sum(nums)
    memo = Hash.new(0)
    nums.each { |v| memo[v] += 1 }
    pos = []
    neg = []
    memo.keys.each { |key| key > 0 ? pos << key : neg << key}
    pos.sort
    neg.sort
    result = []
    if memo.has_key?(0) && memo[0] >= 3
        result << [0, 0, 0]
    end
    neg.each do |a|
        pos.each do |b|
        c = -(a + b)
        if !memo.has_key?(c)
            next
        end
        if c > b
            result << [a, b, c]
        elsif c < a
            result << [c, a, b]
        elsif [a, b].include?(c) && memo[c] > 1
            result << [a, c, b]
        end
        end
    end
    result
end
```

#### Complexity
- Time: O(n^2)
- Space: O(n)
