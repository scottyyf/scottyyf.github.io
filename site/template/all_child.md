# 子集枚举

递归枚举一个组合的所有可能值 模板

回溯的模板

```python
class Solution:
    def test(self, n, k):
        tmp, ret = [], []
        self.dfs(1, n, k, tmp, ret)
        return ret

    def dfs(self, cur_index, n, k, tmp, ret):
        if cur_index > n:
            # 指针指出范围，需要停止
            # 记录答案
            return

        tmp.append(cur_index) # 选取当前值
        self.dfs(cur_index + 1, n, k, tmp, ret) #向前推进

        tmp.pop() # 回溯，不选当前值
        self.dfs(cur_index + 1, n, k , tmp, ret) # 向前推进
```

给定两个整数 n 和 k，返回范围 [1, n] 中所有可能的 k 个数的组合。

你可以按 任何顺序 返回答案。

https://leetcode-cn.com/problems/combinations/

```python
class Solutin:
    def combine(self, n, k):

    def dfs(self, cur, n, k, tmp, ret):
        if len(tmp) == k: # tmp的长度达到要求，则需要停止并记录数据
            tmp = tmp[:] # 由于列表中嵌套列表，存在复制故障，所以这里需要浅拷贝
            ret.append(tmp)
            return

        if cur > n: # 越界
            return

        tmp.append(cur)
        self.dfs(cur+1, n, k, tmp, ret)

        tmp.pop()
        self.dfs(cur+1, n, k, tmp, ret)
```
