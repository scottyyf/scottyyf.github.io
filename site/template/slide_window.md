# 滑动窗口（窗口大小不固定）

* 求子串问题则可用滑动窗口
* 两层while循环：外层遍历数组，内层剔除重复

https://labuladong.gitbook.io/algo/mu-lu-ye-1/mu-lu-ye-3/hua-dong-chuang-kou-ji-qiao-jin-jie

```c
left, right =0, 0
need, window = defaultdict(int), defaultdict(int)

for i in s1:
    need[i] += 1

# 1. 循环条件
while right < size_of_string2:
    # 2 更新window
    window.add(s[right])
    right++

    # 3 缩小window
    while (window need shrink):
        # 4 缩小时更新的数据
        window.remove(s[left])
        left++
```


如求最大不重复子串

```python
from collections import defaultdict


class Solution:
    def test(self, s):
        start,end,max_len = 0,0,0
        counter = 0
        lookup = defaultdict(int)
        while end < len(s):
            lookup[s[end]] += 1
            if lookup[s[end]] > 1:
                counter += 1

            end += 1

            while counter > 0:
                if lookup[s[start]] > 1:
                    counter -= 1

                lookup[s[start]] -= 1
                start += 1
            
            max_len = max(max_len, end-start)

        return max_len
```

最终待模板的样子

```python
class Solution:
    def test(self, s1, s2):
        need, window = defaultdict(int), defaultdict(int)
        left, right = 0, 0
        for c in s2:
            need[c] += 1

        while right < len(s1):
            # c 是加入窗口的字符
            c = s1[right]
            # 右移动窗口
            right += 1

            # 窗口数据更新
            ...

            # debug 位置
            print(left, right)

            # 判断左侧窗口是否要移动
            while (window need shrink):
                # d 是移出的字符
                d = s1[left]
                left += 1

                # 窗口数据的更新
                ...
```
