# Find the Closest Palindrome

#### Description

Given an integer n, find the closest integer (not including itself), which is a palindrome.

The input n is a positive integer represented by string, whose length will not exceed 18.
If there is a tie, return the smaller one as answer.

- Definition

    The 'closest' is defined as absolute difference minimized between two integers.

#### Example
Input: `"123"`

Output: `"121"`

#### How to Solve

The closest palindrome will be created by one of followings:
- a single digit --> subtract 1
- all 9s, --> add 2, for example, 99 -> 101, 999 -> 1001
- a palindrome --> change middle one down (or up if middle is 0)
- others --> replace a right half by a mirror of left half

Check the pattern above one by one would work; however, the code will have many conditions and run slow.

This solution uses a Set to save possible patterns for the first step. In the second step, it checks the value in the Set whether the absolute difference is smaller. If the difference is tie, check the value itself is smaller or not. This way, the solution efficiently finds the result.  

#### Solution
- Python

```python
class ClosestPalindrome:
    def nearestPalindromic(self, n: str) -> str:
        length = len(n)
        closests = set()
        closests.add(pow(10, length) + 1) # if 99, 101 may be the closest
        closests.add(pow(10, length - 1) - 1) # if 100, 99 may be the closest
        prefix = int(n[:((length + 1) // 2)]) # right should be a mirror of left
        for i in [-1, 0, 1]:
            left = str(prefix + i)
            if length % 2 == 0:
                closests.add(int(left + left[::-1]))
            else:
                closests.add(int(left + left[:-1][::-1]))
        num, min_diff = int(n), float('inf')
        if num in closests: closests.remove(num)
        for v in closests:
            diff = abs(v - num)
            if diff < min_diff:
                min_diff = diff
                result = v
            elif diff == min_diff:
                result = min(result, v)
        return str(result)
```

- Ruby

```ruby
# @param {String} n
# @return {String}
def nearest_palindromic(n)
  length = n.size
  closests = Set.new
  closests.add(10 ** length + 1) # if 99, adds 101
  closests.add(10 ** (length - 1) -1) # if 100, adds 99
  prefix = (n[0...((length + 1) / 2)]).to_i
  [-1, 0, 1].each do |i|
    left = (prefix + i).to_s
    if length % 2 == 0
      closests.add((left + left.reverse).to_i)
    else
      closests.add((left + left[0...-1].reverse).to_i)
    end
  end
  num, min_diff, result = n.to_i, 10 ** (length + 1), 0
  closests.delete(num) if closests.include?(num)
  closests.each do |v|
    diff = (v-num).abs
    if diff < min_diff
      min_diff = diff
      result = v
    elsif diff == min_diff
      result = [result, v].min
    end
  end
  result.to_s
end
```

#### Complexity
- Time: O(n) -- n is a length of given string
- Space: O(n)