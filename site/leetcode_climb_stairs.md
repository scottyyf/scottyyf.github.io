# [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs)

要求：

* 每次可爬一步或两步

解法：

暴力法： 这个一个典型的递归性质的问题，根据递归的几个特点

1. 结束条件
2. 处理当前逻辑
3. 下探到下一个处理逻辑
4. 清理状态数据

这里的时间复杂度是O(2^n)，因为每一个逻辑都会变成另外两个逻辑
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 2:
            return 1

        return self.climbStairs(n - 2) + self.climbStairs(n - 1)
```

由于时间复杂度太高，这里需要记录中间状态,所以有下面的动态规划解法
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        dp = {1: 1, 2: 2}
        for i in range(3, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[n]
```

还有一钟方法，找重复性。从小到大，找他的通项公式
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 3:
            return n

        left, mid, right = 1, 2, 3
        for i in range(3, n+1):
            right = left + mid
            left = mid
            mid = right

        return right
```
