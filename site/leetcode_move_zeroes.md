# [移动零](https://leetcode-cn.com/problems/move-zeroes/)

要求：

* 非零数据需要保持原有的顺序
* 不可以额外开辟数据空间

解法：

1. 由于不能改变原有的非零顺序，所以下面的双指针错误. 
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i, j = 0, len(nums) - 1
        while i < j:
            while nums[i] != 0:
                i += 1

            while nums[j] == 0:
                j -= 1

            if i < j:
                nums[i], nums[j] = nums[j], nums[i]
```

2. 由于不可开辟额外空间，所以简单的循环也不适用
3. 使用占位方式，进行替换。遇到0则进行占位，循环过程遇到非0，即和0进行交换
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        first = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[i], nums[first] = nums[first], nums[i]
                first += 1
```
