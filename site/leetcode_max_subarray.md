# [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

要求：

* 求出连续的子序列中，和为最大时的值

1. (错误的做法)想到求装最多水的那道题，使用左右双指针夹逼的方法。如下，这种情况下，如果哪个边界一直大，那么这个边界就一直不会挪动，
导致错误
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        max_value = nums[0]
        while left <= right:
            value = sum(nums[left: right + 1])
            max_value = max(value, max_value)
            if nums[left] < nums[right]:
                left += 1
            else:
                right -= 1

        return max_value
```

2. dp。时间复杂度 O(n),空间复杂度o(n)
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = {0: nums[0]}
        max_value = nums[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i - 1] + nums[i], nums[i])
            max_value = max(max_value, dp[i])

        return max_value
```

3. 优化。因为这里只是要求最大值，步骤2中是把每个位置的值都给缓存了，这个地方可以简化
空间复杂度O(1)
```python
        dp = nums[0]
        max_value = nums[0]
        for i in nums[1:]:
            dp = max(dp + i, i)
            max_value = max(max_value, dp)

        return max_value
```
