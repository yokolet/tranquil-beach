# First Bad Version

#### Description

Imagine, the latest version fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Given n versions [1, 2, ..., n], find out the first bad one, which causes all the following ones to be bad.

Use an API `isBadVersion(version)` which will return whether version is bad. Implement a function to find the first bad version. Minimize the number of calls to the API.

#### Example

```
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
```

#### How to Solve

Like, git bisect, binary search is the approach to find the first bad version. When moving a low or high pointer, check the value before and after a mid position. Then, the next direction will be chosen. 

#### Solution
- Python

```python
# The isBadVersion API is already defined .
# @param version, an integer
# @return a bool
# def isBadVersion(version):

class BadVersion(object):
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 1 and isBadVersion(n): return n
        low, high = 1, n
        while low <= high:
            mid = (low + high) // 2
            result = isBadVersion(mid)
            if result:
                if not isBadVersion(mid - 1):
                    return mid
                high = mid - 1
            else:
                if isBadVersion(mid + 1):
                    return mid + 1
                low = mid + 1
        return mid
```

- Ruby

```ruby
# The is_bad_version API is already defined.
# @param {Integer} version
# @return {boolean} whether the version is bad
# def is_bad_version(version):

# @param {Integer} n
# @return {Integer}
def first_bad_version(n)
  return n if n == 1 && is_bad_version(n)
  low, high = 0, n
  while low <= high
    mid = (low + high) / 2
    is_bad = is_bad_version(mid)
    if is_bad
      if is_bad_version(mid - 1)
        high = mid - 1
      else
        return mid
      end
    else
      if is_bad_version(mid + 1)
        return mid + 1
      else
        low = mid + 1
      end
    end
  end
  mid
end
```

#### Complexity
- Time: O(log(n))
- Space: O(1)