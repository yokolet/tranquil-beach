# Coin Change Patterns

#### Description

Given coins of different denominations and a total amount of money, find the number of combinations that make up that amount.

The patterns can use infinite number of each kind of coins.

#### Example 1
Input: `amount = 5`, `coins = [1, 2, 5]`

Output: 4

Explanation: Four patterns make up the amount:
```
[5]
[2, 2, 1]
[2, 1, 1, 1]
[1, 1, 1, 1, 1]
```

#### Example 2
Input: `amount = 3`, `coins = [2]`

Output: 0

Explanation: Only one coin is 2. No pattern makes up to the amount of 3.

#### Example 3
Input: `amount = 10`, `coins = [10]`

Output: 1

#### How to Solve

This is a typical dynamic programming problem.
The solution here uses an array to save memory.
However, to solve the problem, starting from 2 dimensional array is easier.

Below is a table for the example 1.
The row represents coins, while the column represents amount.
The first row is a base case -- an empty array is given as coins. Only when the amount is 0, one pattern of answer exists.
The second row is for coin = 1.
If `(curret amount - coin value)` is positive or zero,
`memo[prev row][current amount] + memo[current row][current amount - coin value]` will be the value of `memo[current row][current amount]`. If `(curret amount - coin value)` is 0 or negative, copy `memo[prev row][current amount]` to `memo[current row][current amount]`.
The answer is `memo[last row][amount]`.


|   | 0 | 1 | 2 | 3 | 4 | 5 | amount |
|---|---|---|---|---|---|---|--------
| 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 
| 2 | 1 | 1 | 2 | 2 | 3 | 3 |
| 5 | 1 | 1 | 2 | 2 | 3 | 4 |
| coin | | | | | | |


To save memory, this solution does:

```
memo[current row][current amount] = memo[current row][current amount] + memo[current row][current amount - coin value]
```

#### Solution
- Python

```python
class CoinPatterns:
    def change(self, amount: 'int', coins: 'List[int]') -> 'int':
        memo = [0] * (amount + 1)
        memo[0] = 1 # when amount = 0, empty pattern exists
        for coin in coins:
            for i in range(coin, amount + 1):
                if memo[i - coin]:
                    memo[i] += memo[i - coin]
        return memo[amount]
```

- Ruby

```ruby
# @param {Integer} amount
# @param {Integer[]} coins
# @return {Integer}
def change(amount, coins)
  memo = Array.new(amount + 1, 0)
  memo[0] = 1 # when amount = 0, empty pattern exists
  coins.each do |coin|
    (coin..amount).each do |i|
      if memo[i - coin] > 0
        memo[i] += memo[i - coin]
      end
    end
  end
  memo[amount]
end
```

#### Complexity
- Time: O(n*m), n: number of coins, m: amount
- Space: O(m)