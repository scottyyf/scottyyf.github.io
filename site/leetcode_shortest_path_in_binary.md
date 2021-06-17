# [二进制矩阵中的最短路径](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/)

要求：

* nXn的矩阵， 每次可走八方
* 值为1 的地方不可走
* 返回最短路径，否则返回-1

BFS。对于当前格子，使用bfs走完可走的路径，如果可走的路径已经到达终点，那么返回step，否则step+1并继续
```python
class Solution:
    def shortestPathBinaryMatrix(self, grid: list) -> int:
        queue, length = [(0, 0)], len(grid)
        if grid[0][0] or grid[-1][-1]:
            return -1

        if length <= 2:
            return length

        step = 1
        while queue:
            step += 1
            queue_len = len(queue)
            for _ in range(queue_len):
                i, j = queue.pop(0)
                for row, col in [(i - 1, j - 1), (i - 1, j), (i - 1, j + 1),
                                 (i, j - 1), (i, j), (i, j + 1), (i + 1, j - 1),
                                 (i + 1, j), (i + 1, j + 1), ]:
                    if 0 <= row < length and 0 <= col < length and not grid[row][col]:
                        if row == col == length - 1:
                            return step

                        queue.append((row, col))
                        grid[row][col] = 1

        return -1
```
