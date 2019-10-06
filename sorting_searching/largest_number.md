# Largest Number

#### Description

Given an array of non-negative integers, arrange them such that they form the largest number.

#### Example 1
Input: `[10,2]`

Output: `'210'`

#### Exampple 2
Input: `[3,30,34,5,9]`

Output: `'9534330'`

#### How to Solve

This is a string sorting problem. However, it is not a simple sorting since `'3' > '30'` is required. An approache takes here is to add a custom sorting comparator. The solution defines a subclass of Python's str class and overrides the `__lt__` method. The comparison is made between `x+y` and `y+x`. For example, `'3'+'30'` and `'30'+'3'` are compared. The sorted array may start with `'0'`. In this case, multiple `'0'`s may be in the sorted array. For that reason, the string is converted to integer then back to string. 

#### Solution
- Python

```python
class LargestNumber:
    def largestNumber(self, nums: 'List[int]') -> str:

        class Comparator(str):
            def __lt__(self, o):
                return self+o > o+self

        strs = sorted(map(str, nums), key=Comparator)
        return str(int(''.join(strs)))
```

#### Complexity
- Time: `O(nlog(n))` -- n is a length of the given array
- Space: `O(n)`
