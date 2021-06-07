! [三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

DP:down to top.这个题目和机器人从左上角到右下角很像
```python
import copy
class Solution:
    def minimumTotal(self, triangle) -> int:
        # 浅复制只复制做外层的结构，所以内部结构变化，任然会影响被引用对象的值
        dp = copy.deepcopy(triangle)

        # 从倒数第二行，到第0行 这样去计算
        for row in range(len(triangle) - 2, -1, -1):
            for column in range(len(triangle[row])):
                dp[row][column] = min(dp[row + 1][column],
                                      dp[row + 1][column + 1]) + dp[row][column]

        return dp[0][0]
```
