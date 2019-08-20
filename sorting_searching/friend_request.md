# Friends of Appropriate Ages

#### Description

Given a list of positive integers, which represents people's ages, find a total number of friend requests can be made. (`1 <= ages[i] <= 120`)

- Definition

    A person `A` will not make a friend request to a person `B (B != A)` if the conditions below are true.
    - `age[B] <= 0.5 * age[A] + 7`
    - `age[B] > age[A]`
    - `age[B] > 100 && age[A] < 100`

#### Example 1

Input: `[16,16]`

Output: `2`

Explanation: 2 people make friend requests each other.

#### Example 2

Input: `[16,17,18]`

Output: `2`

Explanation: possible friend requets: 17 -> 16, 18 -> 17

#### Example 3

Input: `[20,30,100,110,120]`

Output: `3`

Explanation: possible friend requests: 110 -> 100, 120 -> 110, 120 -> 100

#### How to Solve

Start from creating an age distribution. From the definition, the maximum age is 120. Create an array to save counts of each age. Then go over the age from 15 to 120 for `A`. The starting age of 15 comes from the conditions above. The ages should be `B > A // 2 + 7` and `B <= A`, so 15 is the minimum. For `B`, valid ages are from `A//2+8` to `A`. Loop over this range. Summing up the counts of `A * B` gives the answer. 

#### Solution

- Python

```python
class FriendRequest:
    def numFriendRequests(self, ages: 'List[int]') -> int:
        memo = [0 for _ in range(121)] # 1 <= ages[i] <= 120
        for a in ages:
            memo[a] += 1
        result = 0
        for i in range(15, 121):          # age of A
            if memo[i] == 0: continue
            for j in range(i//2+8, i+1):  # age of B
                if i == j:                # subtract a request to self
                    result += memo[i] * (memo[j] - 1)
                else:
                    result += memo[i] * memo[j]
        return result
```

#### Complexity

- Time: `O(1)` -- two loops are constant, at most 120, no matter how long the ages list is
- Space: `O(1)`