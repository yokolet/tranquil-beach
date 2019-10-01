# Missing Ranges

#### Description

Given a sorted array of integers, `nums`, and inclusive range of `[lower, upper]`, find its missing ranges.

#### Example
Input: `nums=[0,1,3,50,75], lower=0, upper=99`

Output: `["2", "4->49", "51->74", "76->99"]`

#### How to Solve

Ranges between integers in `nums` are easy to handle. If the difference is 2, print one number in-between. If the difference is more than 2, print the range `nums[i-1]+1` to `nums[i]-1`. Something needs to care about is lower and upper bound values. They may or may not be outside of the `nums` range. The solution here appends `lower-1` and `upper+1` to `nums`. By this addition, all missing ranges are found easily.

#### Solution
- Python

```python
class MissingRanges:
    def findMissingRanges(self, nums: 'List[int]', lower: int, upper: int) -> 'List[str]':
        nums = [lower-1] + nums + [upper+1]
        result = []
        for i in range(1, len(nums)):
            if nums[i] - nums[i-1] == 2:
                result.append(str(nums[i]-1))
            elif nums[i] - nums[i-1] > 2:
                result.append('{}->{}'.format(nums[i-1]+1, nums[i]-1))
        return result
```

#### Complexity
- Time: `O(n)` -- n is a length of the given array
- Space: `O(1)`
