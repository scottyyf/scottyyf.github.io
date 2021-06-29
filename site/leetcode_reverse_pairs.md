[翻转对](https://leetcode-cn.com/problems/reverse-pairs/)

要求：

1. 归并排序求次数
```python
class Solution:
    def reverseParis(self, nums: list) -> list:
        self.cnt = 0
        self.sort(nums, 0, len(nums)-1)
        return self.cnt

    def sort(self, nums, left, right):
        if left >= right:
            return

        mid = (left + right) >> 1
        self.sort(nums, left, mid)
        self.sort(nums, mid+1, right)
        self.merge(nums, left, mid, right)

    def merge(self, nums, left, mid, right):
        tmp = []
        i = left
        j = mid + 1
        while i <= mid and j <= right:
            if nums[i] < nums[j]:
                tmp.append(nums[i])
                i += 1
            else:
                tmp.append(nums[j])
                j += 1

        while i <= mid:
            tmp.append(nums[i])
            i += 1

        while j <= right:
            tmp.append(nums[j])
            j += 1
        
        cnt_i, cnt_j = left, mid + 1
        while cnt_i <= mid and cnt_j <= right:
            if nums[cnt_i]/2 <= nums[cnt_j]:
                cnt_i += 1
            else:
                self.cnt += (mid - cnt_i + 1)
                cnt_j += 1

        nums[left: right+1] = tmp
```
