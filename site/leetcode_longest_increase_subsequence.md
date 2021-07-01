# [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

给你一个整数数组 nums ，找到其中最长严格递增子序列的长度。

子序列是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，[3,6,2,7] 是数组 [0,3,1,6,2,2,7] 的子序列。

dp

```python
class Solution:
    def longest_increase_subseq(self, nums: list):
        dp = {0:1}
        for i in range(1, len(nums)):
            tmp = []
            for j in range(0, i):
                if nums[j] < nums[i]:
                    tmp.append(dp[i])
                else:
                    tmp.append(0)

            dp[j] = max(tmp) + 1

        return max(dp.values())
```
