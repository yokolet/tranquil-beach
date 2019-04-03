# Random Pick with Weight

#### Description

Given an array `w `of positive integers, where `w[i]` describes the weight of index i, write a function `pickIndex` which randomly picks an index in proportion to its weight.

```
1 <= w.length <= 10000
1 <= w[i] <= 10^5
```

The function, `pickIndex`, will be called at most 10000 times.


#### Example 1
Input:

```
["Solution","pickIndex"]
[[[1]],[]]
```

Output: `[None,0]`

#### Example 2
Input:

```
["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
```

Output: `[None,0,1,1,1,0]`

#### How to Solve

Create prefix sum from a given weight array. This prefix sum expresses the range of weight. When the weight is big, the range from previous to this value will be big. Given that, randomly generated value will hit such a big range with higher probability.

Once prefix sum is created, do binary search by randomly generated value. To quickly find the result, the solution normalizes the weight from 0 to 1.

#### Solution
- Python

```python
import random

class RandomPick:
    def __init__(self, w: 'List[int]'):
        total = sum(w)
        pvalues = [x/total for x in w]
        psums = [pvalues[0]]
        for p in pvalues[1:]:
            psums.append(p + psums[-1])
        psums[-1] = 1 
        self.psums = psums 

    def pickIndex(self) -> int:
        pick = random.random()
        left, right = 0, len(self.psums) - 1
        while left < right:
            mid = (left + right) // 2
            if pick >= self.psums[mid]:
                left = mid + 1
            else:
                right = mid
        return left
```

- Ruby

```ruby
class RandomPick
=begin
  :type w: Integer[]
=end
  def initialize(w)
    total = w.sum
    pvalues = w.map { |x| x.to_f / total }
    @psums = [pvalues[0]]
    (1...pvalues.size).each do |i|
      @psums << pvalues[i] + @psums[-1]
    end
    @psums[-1] = 1
  end

=begin
    :rtype: Integer
=end
  def pick_index()
    pick = rand
    left, right = 0, @psums.size-1
    while left < right
      mid = (left + right) / 2
      if pick >= @psums[mid]
        left = mid + 1
      else
        right = mid
      end
    end
    left
  end
end
```

#### Complexity
- Time: O(n) and O(log(n))
- Space: O(n)