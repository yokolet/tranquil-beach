# Climbing Stairs

#### Description

Given n, which is a number of stairs, find how many distinct ways to climb up to the top. Each step(s) to climb up can be either 1 or 2.

The given number n is a positive integer,

#### Example 1
Input: 2

Output: 2

Explanation:
- 1 step + 1 step
- 2 steps

#### Example 2
Input: 3

Output: 3

Explanation:
- 1 step + 1 step + 1 step
- 1 step + 2 steps
- 2 steps + 1 step

#### How to Solve

Recursive and dynamic programming approaches are there.
The recursive solution is easy to understand, but runs very slow. For reference, a recursive solution is added to Python code.

The dynamic programming solution runs fast.
The pattern of this kind is:
- save previous states in a variable, array, matrix or other
- set initial state
- compute the rest of all states one by one based on the previous states

In this solution, the previous states are saved in an array, `memo`, of length `n+1`.
The initial states are `memo[0] = 1` (no step, 1 empty set) and `memo[1] = 1` (only 1 step goes to top).
Suppose it's on the ith stair, previous step size was 1 or 2.
So, the sum of `memo[i - 1]` and `memo[i - 2]` will be the value of `memo[i]`. In the end, `memo[n]` holds the answer.

#### Solution
- Python

```python
class Stairs:
    def climbStairsRecur(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n < 0: return 0
        if n == 0: return 1
        sum = 0
        sum += self.climbStairsRecur(n-1)
        sum += self.climbStairsRecur(n-2)
        return sum

    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        memo = [0]*(n+1)
        memo[0] = 1
        memo[1] = 1
        for i in range(2, n+1):
            j = 1
            while j <= 2 and j <= i:
                memo[i] += memo[i-j]
                j += 1
        return memo[n]
```

- Ruby

```ruby
# @param {Integer} n
# @return {Integer}
def climb_stairs(n)
  return 1 if n < 2
  memo = Array.new(n + 1, 0)
  memo[0] = 1
  memo[1] = 1
  (2..n).each do |i|
    j = 1
    while j <= 2 && j <= i
      memo[i] += memo[i - j]
      j += 1
    end
  end
  memo[n]
end
```

#### Complexity
- Recursion
    - Time: O(2^n)
    - Space: O(n)
- Dynamic Programming
    - Time: O(n)
    - Space (n)

    At a glance, time complexity looks O(n^2). However, inner loop runs only twice -- constant time. So, the preformance is O(n).