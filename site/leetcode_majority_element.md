# [多数元素](https://leetcode-cn.com/problems/majority-element/)


要求：

* 找出数组中出现次数大于n/2的数

暴力方法： 穷举并计数统计。时间复杂度O(n)，空间复杂度O(n)
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        dict_data = {}
        popular_num = nums[0]
        max_num = 0
        for num in nums:
            if num not in dict_data:
                dict_data[num] = 1
            else:
                dict_data[num] += 1

            if dict_data[num] >= max_num:
                popular_num = num
                max_num = dict_data[num]

        return popular_num
```
