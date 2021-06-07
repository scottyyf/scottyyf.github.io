# [乘积最大子序和](https://leetcode-cn.com/problems/maximum-product-subarray/)


要求：

1. 连续子序列中，求乘积最大的子序积

乘法中，负数越小再乘以一个负数可能就为最大。这个和求最大和子序列不同

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums:
            return 0

        ret = nums[0]
        min_value = {0:nums[0]}
        max_value = {0:nums[0]}
        for i in range(1, len(nums)):
            max_value[i] = max(max_value[i-1]*nums[i], nums[i], min_value[i-1]*nums[i])
            min_value[i] = min(max_value[i-1]*nums[i], nums[i], min_value[i-1]*nums[i])
            ret = max(ret, max_value[i])

        return ret

```

2. 优化，将max_value这些空间进行优化，并不需要每个节点时的最值
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums:
            return 0

        ret = nums[0]
        min_value = nums[0]
        max_value = nums[0]
        for i in range(1, len(nums)):
            max_tmp, min_tmp = max_value, min_value
            max_value = max(max_tmp * nums[i], nums[i],
                            min_tmp * nums[i])
            min_value = min(max_tmp * nums[i], nums[i],
                            min_tmp * nums[i])
            ret = max(ret, max_value)

        return ret
```
