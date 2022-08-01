# Maximum Swap

#### Description
You are given an integer `num`.
You can swap two digits at most once to get the maximum valued number.

Return the maximum valued number you can get.

#### Examples
##### Example 1
Input: num = `2736`

Output: `7236`

Explanation: Swapping 2 and 7 creates the maximum number.

##### Example 2
Input: num = `9973`

Output: `9973`

Explanation: The given number is already a maximum.

##### Example 3
Input: num = `1993`

Output: `9913`

Explanation: Swapping the second 9 to 1 creates the maximum number.

##### Example 4
Input: num = `98386`

Output: `98836`

Explanation: Swapping the second 8 to 3 creates the maximum number.

#### How to Solve
The problem is easy to understand. However, solving this problem is not so easy.
Swapping number is not always happened to the first digit.
Also, there might be multiple maximum digits, and not the first one will create the maximum number.

Given that, a recursion is a good approach for this problem.
If the first digit should stay on its index, narrowing down to the subarray.
The maximum digit in the subarray should be found from the end of subarray, which
makes the number bigger.

#### Solution
- Python

```python
class MaximumSwap:
    def maximumSwap(self, num: int) -> int:
        def helper(nums):
            if not nums:
                return nums
            max_v = max(nums)
            if nums[0] == max_v:
                return [nums[0]] + helper(nums[1:])
            idx = nums[::-1].index(max_v)
            idx = len(nums) - 1 - idx
            nums[0], nums[idx] = nums[idx], nums[0]
            return nums
        nums = [int(s) for s in str(num)]
        return int("".join([str(d) for d in helper(nums)]))
```

#### Complexity
- Time: `O(n)` -- n is a number of digits in the given number
- Space: `O(n)`
