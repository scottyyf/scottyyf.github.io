# [N皇后](https://leetcode-cn.com/problems/n-queens/)

要求：

* 横竖撇捺都没有两个queen

每次完成一个答案后，继续下一个答案。此时需要清除前面答案的状态，使用回溯

```python
class Solution:
    def solveNQueens(self, n: int):
        self.col, self.pie, self.na = set(), set(), set()
        self.result = []

        self.dfs(n, 0, [])
        return self._generate_result(n)

    def dfs(self, total_n, row, cur_data):
        if row >= total_n:
            self.result.append(cur_data)
            return

        for col in range(total_n):
            if col in self.col or row + col in self.pie or row - col in self.na:
                continue

            self.col.add(col)
            self.pie.add(row + col)
            self.na.add(row - col)

            # 下探
            self.dfs(total_n, row + 1, cur_data + [col])

            # 清除数据
            self.col.remove(col)
            self.pie.remove(row + col)
            self.na.remove(row - col)

    def _generate_result(self, n):
        board = []
        for ret in self.result:
            for col_index in ret:
                board.append('Q'.join(
                    ['.' * col_index, '.' * (n - col_index - 1)]))

        return [board[i:i + n] for i in range(0, len(board), n)]
```
