# 朋友圈问题

要求：

给定一个二维数组，表示人物之前是否是朋友的关系

以下表示AB是朋友，但C不是朋友，求当前所有关系中存在朋友圈的个数，这里应返回2

| | A | B | C |
| - | - | - | - |
| A | 1 | 1 | 0 |
| B | 1 | 1 | 0 |
| C | 0 | 0 | 1 |

1. DFS方法，这个类似岛屿问题，个人认为这种解法就像扩散污染一样。每次都将能污染的地方都污染掉，下一次递归再污染其他没有污染的地方

```python
class solution:
    def find_circle_num(self, M: list):
        visited = [0] * len(M)
        count = 0
        for row in range(len(M)):  # 每个人
            if visited[row] == 0:
                self.dfs(M, visited, row)
                count += 1

        return count

    def dfs(self, M: list, visited: list, row: int):
        # 污染一个人并扩散到朋友圈
        for col in range(len(M)):  # 每个人的朋友圈进行污染
            if visited[col] == 0 and M[row][col] == 1:
                visited[col] = 1
                self.dfs(M, visited, col)  # 对col对应的朋友进行污染
```

2. 朋友圈个数使用并查集，求并查集剩余的头的数量即为朋友圈个数
```python
class Solution2(Solution):
    def findCircleNum(self, m: list):
        if not m or not m[0]:
            return 0

        p = [i for i in range(len(m))]
        for row in range(len(m)):
            for col in range(len(m[0])):
                if m[row][col] == 1:
                    self.union(p, row, col)

        return len(set([self.parent(p, i) for i in range(len(m))]))

    def union(self, p, row, col):
        row_parent = self.parent(p, row)
        col_parent = self.parent(p, col)
        if row_parent != col_parent:
            p[row_parent] = col_parent

    def parent(self, p, row):
        root = row
        while p[root] != root:
            root = p[root]

        while p[row] != row:
            x = row
            row = p[row]
            p[x] = root

        return root
```

