# Best Time to Buy and Sell Stock

#### Description

Given an array of integers whose ith element is a stock price on day i, find the maximum profit.

At most one transaction is allowed. The transaction means: buy one and sell one share of stock.

The stock must be bought before it is sold.

#### Example 1
Input: [7,1,5,3,6,4]

Output: 5

#### Example 2
Input: [7,6,4,3,1]

Output: 0

#### How to Solve

Keep track the minimum price.
If the price at index i is lower than the current minimum, update the minimum price. At each index, compare (current price - minimum price) and profit so far. Update if the value is greater than the profit so far.

#### Solution
{% code-tabs %}

{% code-tabs-item title=Python %}
```python
class Stock:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        min_price = float('inf')
        profit = 0
        for i in range(len(prices)):
            if prices[i] < min_price:
                min_price = prices[i]
            elif prices[i] - min_price > profit:
                profit = prices[i] - min_price
        return profit
```
{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}
```ruby
# @param {Integer[]} prices
# @return {Integer}
def max_profit(prices)
  return 0 if prices.nil? || prices.empty?
  min_price = prices.shift
  profit = 0
  prices.each do |p|
    if p < min_price
      min_price = p
    elsif p - min_price > profit
      profit = p - min_price
    end
  end
  profit
end
```
{% endcode-tabs-item %}

{% endcode-tabs %}

#### Complexity
- Time: O(n)
- Space: O(1)