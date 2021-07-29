# [打家劫舍](https://leetcode-cn.com/problems/house-robber/)

要求

* 不能连续偷两家，只能间断偷

dp, 最后一步： 偷了ak， 那么只能加f(k-2)的值；否则只能算f(k-1)的值

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0

        if len(nums) < 2:
            return nums[0]

        dp = [0] * len(nums)
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])
        for house in range(2, len(nums)):
            dp[house] = max(dp[house - 2] + nums[house], dp[house - 1])

        return dp[len(nums) - 1]
```

# [打家劫舍2]()

* 要求：除不能连续偷两家外，还得不允许偷手尾两家

```python
class Solution:
    def rob(self, nums) -> int:
        length = len(nums)
        if length == 1:
            return nums[0]

        if length == 2:
            return max(nums)

        return max(self.rob_circle(0, length - 2, nums),
                   self.rob_circle(1, length - 1, nums))

    def rob_circle(self, start: int, end: int, nums: list):
        dp = [0] * len(nums)
        dp[start] = nums[start]
        dp[start + 1] = max(nums[start], nums[start + 1])
        for i in range(start + 2, end + 1):
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1])

        return dp[end]
```
