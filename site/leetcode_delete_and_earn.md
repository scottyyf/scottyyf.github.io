# 删除并获取点数

给你一个整数数组 nums ，你可以对它进行一些操作。

每次操作中，选择任意一个 nums[i] ，删除它并获得 nums[i] 的点数。之后，你必须删除 所有 等于 nums[i] - 1 和 nums[i] + 1 的元素。

开始你拥有 0 个点数。返回你能通过这些操作获得的最大点数。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/delete-and-earn

这里把nums[i],nums[i-1],nums[i+1]看做是打家劫舍的变形题

```python
class Solution:
    def delete_and_earn(self, nums):
        tmp_nums = [0] * (max(nums)+1)
        dp = {0: 0,1:tmp_nums[1]}
        for i in range(2， len(tmp_nums)):
            dp[i] = max(dp[i-1], dp[i-2]+tmp_nums[i]*i)

        return dp[len(tmp_nums)-1]
```
