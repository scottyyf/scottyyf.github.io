# [解数独](https://leetcode-cn.com/problems/sudoku-solver/#/description)

要求：

* 给出部分数字，要求完成真个数独

这里采用回溯，同时要防止人肉进行递归
```python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or len(board) == 0:
            return

        self.helper(board)

    def helper(self, board):
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] != '.':
                    continue

                for c in range(1, 10):
                    if self.is_valid(board, i, j, str(c)):
                        board[i][j] = str(c)

                        if self.helper(board):
                            return True
                        else:
                            board[i][j] = '.'

                return False

        return True

    def is_valid(self, board, row, col, chart):
        for i in range(9):
            if board[i][col] != '.' and board[i][col] == chart:
                return False
            if board[row][i] != '.' and board[row][i] == chart:
                return False
            if board[row // 3 * 3 + i // 3][col // 3 * 3 + i % 3] != '.' and \
                    board[row // 3 * 3 + i // 3][col // 3 * 3 + i % 3] == chart:
                return False
        return True
```


别人写的和N皇后类似结构的代码.
```python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        rows = [set(range(1, 10)) for _ in range(9)]
        cols = [set(range(1, 10)) for _ in range(9)]
        blocks = [set(range(1, 10)) for _ in range(9)]

        empty = []
        for i in range(9):
            for j in range(9):
                if board[i][j] != '.':
                    val = int(board[i][j])
                    rows[i].remove(val)
                    cols[j].remove(val)
                    blocks[i // 3 * 3 + j // 3].remove(val)
                else:
                    empty.append((i, j))

        self.backtrace(board, 0, empty, rows, cols, blocks)

    def backtrace(self, board, level, empty, rows, cols, blocks):
        if level == len(empty):
            return True

        i, j = empty[level]
        b = i // 3 * 3 + j // 3
        for val in rows[i] & cols[j] & blocks[b]:
            rows[i].remove(val)
            cols[j].remove(val)
            blocks[b].remove(val)

            board[i][j] = str(val)

            if self.backtrace(board, level+1, empty, rows, cols, blocks):
                return True

            rows[i].add(val)
            cols[j].add(val)
            blocks[b].add(val)

        return False
```
