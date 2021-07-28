## 列表去重

只允许在原数组上进行去重，不开空间

做法是： 将不重复的数字放到前面去,然后删除结尾重复的数字

```python
class Solution:
    def remove_dup_from_array(self, nums):
        slow, fast = 0, 1
        # 移动不重复的数字
        while fast < len(nums):
            if nums[fast] not in nums[:slow + 1]:
                slow += 1
                nums[slow] = nums[fast]

            fast += 1

        # 删除重复的结尾数字
        for _ in range(fast - slow - 1):
            nums.pop()

        return nums
```
