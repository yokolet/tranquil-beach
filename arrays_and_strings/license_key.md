# License Key Formatting

#### Description

Given a license key represented as a string S and an integer K,
reformat the license key such that it forms groups of exactly K characters except the first one (may shorter). The groups are connected by a dash and have uppercase and digit letters.

#### Example 1

Input: `S = "5F3Z-2e-9-w", K = 4`

Output: `"5F3Z-2E9W"`

#### Example 2

Input: `S = "2-5g-3-J", K = 2`

Output: `"2-5G-3J"`

#### How to Solve

The dashes in the input string should be removed.
Then, the string is checked from last to first.
To make reverse traversal easy, the string is reversed and a chunk of K is added to the array.
In the end, strings in the array are connected by the dash and reversed.

#### Solution

- Python

```python
class LicenseKey:
    def licenseKeyFormatting(self, S: str, K: int) -> str:
        S = ''.join(S.upper().split('-'))[::-1]
        result = []
        for i in range(0, len(S), K):
            result.append(S[i:i+K])
        return '-'.join(result)[::-1]
```

#### Complexity

- Time: `O(n)` -- n is a length of input array since K may be 1
- Space: `O(n)`