# [字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)

两遍扫描，返回结果
```python
class Solution:
    def test(self, s: str) -> int:
        tmp = {}
        for _s in s:
            tmp[_s] = tmp.setdefault(_s, 0) + 1

        for i in range(len(s)):
            if tmp[s[i]] == 1:
                return i
        return -1
```

模拟队列先进先出
```python
class Solution:
    def test(self, s: str) -> int:
        positon = {}
        queue = []
        for i, v in enumarate(s):
            if v not in positon:
                positon[v] = i
                q.append((i, v))
            else:
                position[v] = -1
                while queue and positon[queue[0][1]] == -1:
                    queue.pop(0)
        
        return queue[0][0] if queue else -1
```
