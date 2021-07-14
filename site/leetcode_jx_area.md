# 矩形的最大面积

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。求在该柱状图中，能够勾勒出来的矩形的最大面积。

1. 暴力法
```python
class Solution:
    def largest(self, heights):
        max_area = 0
        for i in range(len(heights)):
            left, right = i, i
            while left >= 0 and heights[left] >= heights[i]:
                left -= 1

            while right <= len(heights)-1 and heights[right] >= heights[i]:
                right += 1

            max_area = max(max_area, heights[i]*(right-left-1))

        return max_area
```

2. 栈的方法
```python
class Solution:
    def largest(self, heights):
        max_area = 0
        stack = []
        for i in range(len(heights)):
            while len(stack) > 0 and heights[i] > stack[-1][1]:
                curr_height = stack[-1][1]
                stack.pop()
                if stack:
                    curr_width = i - stack[-1][0] - 1
                else:
                    curr_width = i

                max_area = max(max_area, curr_height * curr_width)

            stack.append([i, heights[i])

        while stack:
            curr_height = stack[-1][1]
            stack.pop()
            if stack:
                curr_width = len(heights) - stack[-1][0]
            else:
                curr_width = len(heights)

            max_area = max(max_area, curr_heights * curr_width)

       return max_area
```
