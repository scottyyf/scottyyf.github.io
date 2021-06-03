# [不同路径](https://leetcode-cn.com/problems/unique-paths/solution/bu-tong-lu-jing-by-leetcode-solution-hzjf/)

要求：

* 从start位置到end位置，可左走和右走，求路径数量

从上往下
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0 for _ in range(n)] for _ in range(m)]

        for row in range(m):
            for column in range(n):
                if row == 0 or column == 0:
                    dp[row][column] = 1

                else:
                    dp[row][column] = dp[row - 1][column] + dp[row][column - 1]

        return dp[m-1][n-1]
```

# [不同路径2]()

以下这个解法和上面的是同一个思想。对于不可达的，第一行和第一列需要判断能否到达，而不能直接赋值1

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        dp = [[0 for _ in range(n)] for _ in range(m)]

        dp[0][0] = 1 if obstacleGrid[-1][-1] == 0 else 0
        # 判读行的赋值
        for i in range(1, m):
            if obstacleGrid[i][0] == 1 or dp[i-1][0] == 0:
                dp[i][0] = 0
            else:
                dp[i][0] = 1

        # 判断列的赋值
        for i in range(1, n):
            if obstacleGrid[0][i] == 1 or dp[0][i-1] == 0:
                dp[0][i] = 0
            else:
                dp[0][i] = 1

        for row in range(1, m):
            for column in range(1, n):
                if obstacleGrid[row][column] == 1:
                    dp[row][column] = 0
                else:
                    dp[row][column] = dp[row - 1][column] + dp[row][column - 1]

        return dp[m - 1][n - 1]
```

下面这个是优化版本，上面的版本会超时

这里的dp[j] = dp[j] + dp[j-1] 指的是j列和j-1列

时间复杂度O(mn) 空间复杂度O(n)
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        dp = [0] * n

        dp[0] = 1 if obstacleGrid[0][0] == 0 else 0
        for row in range(m):
            for column in range(n):
                if obstacleGrid[row][column] == 1:
                    dp[column] = 0
                elif column >= 1:
                    dp[column] = dp[column] + dp[column - 1]

        return dp[n - 1]
```
