# Accounts Merge

#### Description

Given a list of accounts, merge those accounts. Each element `accounts[i]` is a list of strings, where the first element is a name and the rest are emails. If one of the email is found in another account, merge those two accounts. When accounts can be merged, the name should be the same.

The merged accounts have the format: the first element is a name, the rest are sorted emails. The order of accounts doesn't matter.

#### Example

Input:

```
[
    ["John", "johnsmith@mail.com", "john00@mail.com"],
    ["John", "johnnybravo@mail.com"],
    ["John", "johnsmith@mail.com", "john_newyork@mail.com"],
    ["Mary", "mary@mail.com"]
]
```

Output:

```
[
    ["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],
    ["John", "johnnybravo@mail.com"],
    ["Mary", "mary@mail.com"]
]
```

#### How to Solve

The union-find is a good approach to solve this problem. Create an array of group id, whose elements have their indices at the beginning. The group id corresponds to account index. When the same email is found, find the parents of two groups and union them.

After all group ids are updated, merge emails. Find each account's parent and merge emails to the parent account. At the end, take a set and sort emails.

#### Solution

- Python

```python
class AccountMerge:
    def accountsMerge(self, accounts: 'List[List[str]]') -> 'List[List[str]]':
        n = len(accounts)
        memo = {}
        group = [i for i in range(n)]

        def find(p):
            while p != group[p]:
                p = group[p]
            return p

        def union(x, y):
            x, y = find(x), find(y)
            if x != y:
                min_p, max_p = min(x, y), max(x, y)
                group[max_p] = min_p

        for i in range(n):
            for e in accounts[i][1:]:
                if e in memo:
                    union(i, memo[e])
                else:
                    memo[e] = i

        for i in range(len(group)):
            if i != group[i]:
                p = find(group[i])
                for e in accounts[i][1:]:
                    accounts[p].append(e)
                accounts[i] = None

        return [[a[0]]+sorted(set(a[1:])) for a in accounts if a]
```

#### Complexity

- Time: `O(m*log(n))` -- m is a length of the accounts, n is a number of groups
- Space: `O(m)`