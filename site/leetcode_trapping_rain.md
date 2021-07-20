# 接雨水

O(N) stack

```python
class Solution:
    def trap(height):
        res = 0
        stack = []
        for k, v in enumerate(height):
            while stack and v > stack[-1][1]:
                top_k, top_v = stack.pop()
                if not stack:
                    continue

                left_k, left_v = stack[-1]
                width = k - left_k - 1
                h = min(v, left_v) - top_v
                res += width * h

            stack.append([k, v])

        return res
```

