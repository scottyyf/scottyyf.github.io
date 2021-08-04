# 滑动窗口

给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位
 
返回滑动窗口中的最大值。

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

给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。


示例 1:

输入: s = "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters

```python
from collections import defaultdict

class Solution:
    def test(self, s):
        start, end, max_len = 0, 0, 0
        lookup = defaultdict(int)

        while end < len(s):
            if lookup[s[end]] > 0:
                counter += 1

            lookup[s[end]] += 1
            end += 1
            while counter > 0:
                if lookup[s[start]] > 1:
                    counter -= 1

                lookup[s[start]] -= 1
                start += 1

            max_len = max(max_len, end-start)

        return max_len
```
