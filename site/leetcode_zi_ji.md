# [子集](https://leetcode-cn.com/problems/subsets/solution/zi-ji-by-leetcode-solution/)

要求：

列出所有的子集列表

递归分治
```python
class Solution:
    def subsets(self, nums):
        ans, tmp_list = [], []
        if not nums:
            return ans

        self.dfs(ans, nums, tmp_list, 0)
        return ans

    def dfs(self, ans: list, nums: list, tmp_list: list, index):
        if index == len(nums):
            ans.append(tmp_list[:]) # 浅复制
            return

        self.dfs(ans, nums, tmp_list, index + 1)

        tmp_list.append(nums[index])
        self.dfs(ans, nums, tmp_list, index + 1)
        tmp_list.pop()
```

或者不需要tmp_list.pop，那么需要每个调用的地方给复制下
```python
class Solution:
    def subsets(self, nums):
        ans, tmp_list = [], []
        if not nums:
            return ans

        self.dfs(ans, nums, tmp_list, 0)
        return ans

    def dfs(self, ans: list, nums: list, tmp_list: list, index):
        if index == len(nums):
            ans.append(tmp_list)
            return

        self.dfs(ans, nums, tmp_list[:], index + 1)

        tmp_list.append(nums[index])
        self.dfs(ans, nums, tmp_list[:], index + 1)
```

迭代： 考虑的思路是： 都没有， 有1， 有2, 有3, 有n 每个有都是独立的
```python
class Solution:
    def subsets(self, nums):
        res = [[]]
        for i in nums:
            res = res + [[i] + num for num in res]

        return res
```
