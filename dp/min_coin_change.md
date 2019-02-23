# Minimum Coin Change

#### Description

Given coins of different denominations and a total amount of money amount, the fewest number of coins to make up the amount.
Return -1 if the amount is unable to be made up.

#### Example 1
Input: `coins = [1, 2, 5]`, `amount = 11`

Output: 3

Explanation: `[5, 5, 1]` is the fewest

#### Example 2
Input: `coins = [2]`, `amount = 3`

Output: -1

#### How to Solve

Dynamic programming approach is popular for this.
The solution here uses an arry for memory saving, however,
thinking in 2 dimensional array (table) is easier to understand.

This problem is asking a minimum number of coin combination.
If possibile, initialize the array by a max integer. Ruby doesn't have such value, so Ruby code uses -1 for the initial value. Ruby code has additional condition to know the value is smaller or not handled yet.

The table below shows how each cells are filled out.
The first row is the initial state.
The second row is the state of the coin value 1.
For example, to calcuate (1, 1) cell, compare the value above row, inf, and the value of the same row's (amount - coin value) cell plus one. Take smaller. Another position is, for example, cell (5, 5). The value of (amount - coin value) + 1 is 1, and above rows is 3. The smaller is 1.

Like this way, using prvious states, next state will be calculated. The answer is in the cell, (5, 11), which is 3.


|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | amount |
|---|---|---|---|---|---|---|---|---|---|---|----|----|--------|
| 0 | 0 |inf|inf|inf|inf|inf|inf|inf|inf|inf|inf |inf ||
| 1 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 ||
| 2 | 0 | 1 | 1 | 2 | 2 | 3 | 3 | 3 | 4 | 4 | 4  | 5  ||
| 5 | 0 | 1 | 1 | 2 | 2 | 1 | 2 | 2 | 3 | 3 | 2  | 3  ||
| coin | | | | | | |


#### Solution
- Python

```python
class MinCoinChange:
    def coinChange(self, coins: 'List[int]', amount: 'int') -> 'int':
        memo = [float('inf')] * (amount + 1)
        memo[0] = 0
        for coin in coins:
            for i in range(1, amount + 1):
                if coin <= i and (memo[i - coin] + 1 < memo[i]):
                    memo[i] = memo[i - coin] + 1
        return -1 if memo[amount] == float('inf') else memo[amount]
```

- Ruby

```ruby
# @param {Integer[]} coins
# @param {Integer} amount
# @return {Integer}
def coin_change(coins, amount)
  memo = Array.new(amount + 1, -1)
  memo[0] = 0
  coins.each do |coin|
    (1..amount).each do |i|
      if coin <= i && memo[i - coin] > -1
        memo[i] = memo[i - coin] + 1 if memo[i] == -1 || memo[i - coin] + 1 < memo[i]
      end
    end
  end
  memo[amount]
end
```

#### Complexity
- Time: O(n*m), n: number of coins, m: amount
- Space: O(m)