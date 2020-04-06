# Hand of Straights

#### Description

Given an array of integers called hand which represent cards, rearrange the cards into groups so that each group is size `W` and consists of `W` consecutive cards. Return `True` if and only if it's possible.

#### Example 1

Input: `hand = [1,2,3,6,2,3,4,7,8], W = 3`

Output: `True`

Explanation: hand can be rearranged as `[1,2,3],[2,3,4],[6,7,8]`.

#### Example 2

Input: `hand = [1,2,3,4,5], W = 4`

Output: `False`

#### Example 3

Input: `hand = [2,4,6], W = 3`

Output: `False`

#### How to Solve

The first step is to count each card. If the hand has two `1`s, `2` and `3` should exist at least two in the hand. The solution iterates distinct cards in the sorted order. The necessary number of cards is subtructed from expected consecutive cards. If the consecutive card does not exist or enough number of cards are not left, the answer is false. If all distinct cards are checked, the answer is true.

#### Solution
- Python

```python
from collections import defaultdict

class HandOfStraights:
    def isNStraightHand(self, hand: 'List[int]', W: int) -> bool:
        if W == 1: return True
        if len(hand) % W != 0: return False
        num_dict = defaultdict(int)
        for num in hand:
            num_dict[num] += 1
        for n in sorted(set(hand)):
            count = num_dict[n]
            if count == 0: continue
            for i in range(n, n+W):
                if i not in num_dict or num_dict[i] < count: return False
                num_dict[i] -= count
        return True
```

#### Complaxity
- Time: `O(nlog(n))` -- n is a number of distinct cards
- Space: `O(n)`