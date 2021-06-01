# [盛更多的水](https://leetcode-cn.com/problems/container-with-most-water)

要求：

* 给出列表，以index为x轴，value为y轴，生成一个类似水桶的空间

解法：

暴力法： 时间复杂度O(n^2)
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_area = 0
        for left in range(len(height) - 1):
            for right in range(left + 1, len(height)):
                area = (right - left)*min(height[left], height[right])
                max_area = max(area, max_area)

        return max_area
```

双指针法：时间复杂度O(n),左右两边谁的值小，谁就向对向靠拢
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_area = 0
        while left < right:
            if height[right] < height[left]:
                max_area = max(max_area, (right - left) * height[right])
                right -= 1
            else:
                max_area = max(max_area, (right - left) * height[left])
                left += 1

        return max_area
```
