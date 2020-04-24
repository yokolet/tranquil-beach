# Bulls and Cows

#### Description

Given two strings, `secret` and `guess`, count bulls and cows. Return the result as a string `"nAmB"` where n and m are numbers of bulls and cows respectively.

- Definition
    - If the letter in the `guess` appers on the same index in `secret` , it is a bull.
    - If the letter in the `guess` exists in the `secret` but not the same index, it is a cow.
    - If the letter is cow but the number of the letter exceeds the one in `secret`, don't count the excess as cow.

#### Example 1

Input: `secret = "1807", guess = "7810"`

Output: `"1A3B"`

Explanation: bull: 1, cows, 0, 1, 7

#### Example 2

Input: `secret = "1123", guess = "0111"`

Output: `"1A1B"`

Explanation: bull: the 1st 1, cows: the 2nd (or 3rd) 1

#### How to Solve

Go over two strings once to count bulls. Then, find the intersection of the two strings. The sum of all counts in the intersection includes bulls, so subtract the number of bulls. It is the cows.

#### Solution
- Python

```python
from collections import Counter

class BullsCows:
    def getHint(self, secret: str, guess: str) -> str:
        b = 0
        for i in range(len(secret)):
            if secret[i] == guess[i]:
                b += 1
        sc = Counter(secret)
        gc = Counter(guess)
        cs = sc & gc
        return "{}A{}B".format(str(b), str(sum(cs.values()) - b))
```

#### Complexity
- Time: `O(n)` -- n is a length of a given string
- Space : `O(n)`
