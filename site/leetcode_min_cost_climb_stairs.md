# [使用最小花费爬楼梯](https://leetcode-cn.com/problems/min-cost-climbing-stairs/)

要求：

* 起始位置从0或1开始
* 进过对应的cost消耗对应的体力cost[i]值

```python
class Solution:
    def min_cost(self, cost:list) -> int:
        dp = {0:0, 1:0}
        n = len(cost)
        for step in range(2, n+1):
            dp[step] = min(dp[step-1]+cost[step-1], dp[step-2]+cost[step-2])

        return dp[n]
```

加一个要求，将具体路径打印出来。这里dp好像也是可以的
```python
class Solution:
    def minCostClimbingStairs(self, cost: list) -> int:
        dp = {0: 0, 1: 0}
        step = []
        for i in range(2, len(cost)+1):
            if dp[i-1] + cost[i-1] <= dp[i-2]+cost[i-2]:
                dp[i] = dp[i-1] + cost[i-1]
                if i-1 not in step:
                    step.append(i-1)
            else:
                dp[i] = dp[i-2]+cost[i-2]
                if i-2 not in step:
                    step.append(i-2)
        print(step)
        return dp[len(cost)]
```
