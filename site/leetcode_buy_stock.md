# 买卖股票问题

### 121. 买卖股票的最佳时机
给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock

1. 股票可能是一直下跌的，所以不能直接用max - min
2. 获利最大利益是：最低点买，最高点卖，就一次买和卖
3. 这个不是多次买卖

```python
class Solution:
    def max_profit(self, prices):
        if len(prices) < 2:
            return 0

        min_price = prices[0]
        dp = {0: 0}
        for i in range(1, len(prices)):
            min_prices = min(prices[i], min_prices)
            dp[i] = max(dp[i-1], prices[i] - min_prices)
```

### 122. 买卖股票的最佳时机 II

给定一个数组 prices ，其中 prices[i] 是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii

1. 这个是多次买卖
2. 既然是多次买卖，那么我就可以只算每次涨的钱数，他们的和就是我赚的最大值
3. 或者二维dp，dp[i][0]表示我不持有股票，dp[i][1]表示持有

```python
class Solution:
    def max_profit(self, prices):
        dp = [[0, 0] for _ in range(len(nums))]
        dp[0][0] = 0 # 不买就不赚不亏
        dp[0][1] = -prices[0]  # 买了股票，所以赚的钱为负，买了东西了

        for i in range(1, len(prices)):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
            dp[i][1] = max(dp[i-1][0] - prices[i], dp[i-1][1])
        
        return dp[-1][0]  #返回最后手上没有股票时赚的钱
```

