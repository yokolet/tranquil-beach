# Jewels in Stones

#### Description

Given two strings, J and S, whose characters represent jewels and stones respectively, find how many jewels are in stones.

The characters in J are distinct. All characters in J and S are letters and case sensitive.

#### Example 1

Input: `J = 'aA', S = 'aAAbbbb'`

Output: `3`

#### Example 2

Input: `J = 'z', S = 'ZZ'`

Output: `0`

#### How to Solve

Just go over stone characters and check whether each char is in J or not. If the char included in J, count up.


#### Solution

- Python

```python
class JewelsInStones:
    def numJewelsInStones2(self, J: str, S: str) -> int:
        count = 0
        for s in S:
            if s in J: count += 1
        return count
```

#### Complexity

- Time: O(n) -- n is lengths of S
- Space: O(1)