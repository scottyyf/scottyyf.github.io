## 旋转数组

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/rotate-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```python
class Solution:
    def rotate(self, nums, k):
        k = k % len(nums)
        pos_cut = len(nums) - k
        nums[:] = nums[pos_cut:] + nums[:pos_cut]
```

* 多次翻转

```python
class Solution:
    def rotate(self, nums: list, k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        self.scott_reverse(nums, 0, len(nums) - 1)
        self.scott_reverse(nums, 0, k % len(nums) - 1)
        self.scott_reverse(nums, k % len(nums), len(nums) - 1)

    def scott_reverse(self, a_list: list, start, end):
        while start < end:
            a_list[start], a_list[end] = a_list[end], a_list[start]
            start += 1
            end -= 1
```
