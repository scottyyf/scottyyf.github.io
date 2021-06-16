# [有效的数独](https://leetcode-cn.com/problems/valid-sudoku/description/)

要求：

* 横，竖， 方格 没有重复的数字

全局搜索

```python
class Solution:
    def isValidSudoku(self, board) -> bool:
        rows, cols, boxes = [{} for i in range(9)],\
                            [{} for i in range(9)],\
                            [{} for i in range(9)]

        for row in range(9):
            for col in range(9):
                num = board[row][col]
                if num == '.':
                    continue

                box_index = (row // 3) * 3 + col // 3

                rows[row][num] = rows[row].get(num, 0) + 1
                cols[col][num] = cols[col].get(num, 0) + 1
                boxes[box_index][num] = boxes[box_index].get(num, 0) + 1

                if boxes[box_index][num] > 1 or \
                        rows[row][num] > 1 or \
                        cols[col][num] > 1:
                    return False

        return True
```
