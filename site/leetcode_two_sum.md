# [两数之和](https://leetcode-cn.com/problems/two-sum)

要求：

* 输入一个列表，一个target，返回列表中和为target时的index

解法：

暴力法： 时间复杂度O(n^2)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for left in range(len(nums)-1):
            for right in range(left + 1, len(nums)):
                _sum = nums[left] + nums[right]
                if _sum == target:
                    return [left, right]

        return []
```

附：通过一维变二维，以及空间换时间的套路进行优化。

将已经遍历过的数据存起来，以供后面使用
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        exist_data = {}
        for i in range(len(nums)):
            other_data = target - nums[i]
            if other_data in exist_data:
                return [exist_data[other_data], i]

            exist_data[nums[i]] = i

        return []
```
