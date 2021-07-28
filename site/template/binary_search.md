## 二分查找
* 被查找的数据是有序的

```python
class Solution:
    def binary_search(self, nums, target):
        left, right = 0, len(nums)-1
        while left <= right:
            pivot = left + (right - left) // 2
            if nums[pivot] == target:
                return pivot
            elif nums[pivot] > target:
                right = pivot - 1
            else:
                left = pivot + 1

        return -1
```
