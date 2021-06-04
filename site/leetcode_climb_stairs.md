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

正儿八经的动态规划
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        ret_list = {}
        return self.climb(n, ret_list)

    def climb(self, n, ret: dict):
        if n < 3:
            return n

        if n in ret:
            return ret[n]

        ret[n] = self.climb(n - 1, ret) + self.climb(n - 2, ret)
        return ret[n]
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

> **_NOTE:_**  如果可以走三步，那么函数是怎样的

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        dp = {0: 0, 1: 1, 2: 2, 3: 4}
        for stair in range(4, n + 1):
            dp[stair] = dp[stair - 1] + dp[stair - 2] + dp[stair - 3]

        return dp[n]
```

> **_NOTE:_**  如果相邻两步不能相同又是怎样的呢

相邻两步不能相同。上一步骤的状态可用二维数据的二维记录。如dp[n][1] 表示爬n阶时，走的是一部，那么dp[n-1]时就只能dp[n-1][2]和dp[n-1][3]
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # dp = {0: 0, 1: 1, 2: 2, 3: 3}
        dp = [[0] * 4 for _ in range(n + 1)]
        dp[1][1] = 1
        dp[2][2] = 1
        dp[3][1] = 1
        dp[3][2] = 1
        dp[3][3] = 1
        for stair in range(4, n + 1):
            if stair > 1:
                dp[stair][1] = dp[stair - 1][2] + dp[stair - 1][3]
            if stair > 2:
                dp[stair][2] = dp[stair - 2][1] + dp[stair - 2][3]
            if stair > 3:
                dp[stair][3] = dp[stair - 3][1] + dp[stair - 3][2]

        return dp[n][1] + dp[n][2] + dp[n][3]
```

