# 滑动窗口

O(N)

```python
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums, k):
        bigger = deque()
        ret = []
        for i, v in enumerate(nums):
            while bigger and v > nums[bigger[-1]]:
                bigger.pop()

            bigger.append(i)
            if i - bigger[0] >= k:
                bigger.popleft()

            if i + 1 >= k:
                ret.append(nums[bigger[0]])

        return ret
```

O(N*K)

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        ret = []
        for i in range(k-1, len(nums)):
            ret.append(max(nums[i-k+1:i+1]))

        return ret
```
