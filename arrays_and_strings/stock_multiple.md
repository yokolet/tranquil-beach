# Best Time to Buy and Sell Stock 2 - Multiple Times

#### Description

Given an array of integers whose ith element is a stock price on day i, find the maximum profit.

As many as possible transactions are allowed. The transaction means: buy one and sell one share of stock.

The stock must be bought before it is sold.

#### Example 1
Input: [7,1,5,3,6,4]

Output: 7

Explanation: buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4. buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

#### Example 2
Input: [7,6,4,3,1]

Output: 0

Explanation: the prices ever decrease. There's no index to make a profit.

#### How to Solve

Compare each price to the previous one. If the difference is greater than the previous day, add up the difference as a profit. This is the equivalent to find a profittable range.

#### Solution
- Python

```python
class StockMultiple:
    def maxProfit(self, prices: 'List[int]') -> int:
        if len(prices) <= 1: return 0
        profit = 0
        for i in range(1, len(prices)):
            profit += max(prices[i] - prices[i-1], 0)
        return profit
```

#### Complexity
- Time: `O(n)`
- Space: `O(1)`
