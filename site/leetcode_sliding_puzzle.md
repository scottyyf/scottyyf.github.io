# [滑动谜题](https://leetcode-cn.com/problems/sliding-puzzle/)

要求：

* 求最少步骤可完成6puzzle的问题

单纯的BFS
```python
class Solution:
    def slidingPuzzle(self, board: List[List[int]]):
        puzzle_map = {
            0: [1, 3],
            1: [0, 2, 4],
            2: [1, 5],
            3: [0, 4],
            4: [1, 3, 5],
            5: [2, 4]
            }

        visited = []
        step = 0
        begin_str = ''.join(str(c) for row in board for c in row)
        queue = [begin_str]
        while queue:
            for _ in range(len(queue)):
                s = queue.pop(0)
                if s == '123450':
                    return step

                visited.append(s)
                zero_index = s.index('0')
                arr = list(s)
                for move in puzzle_map[zero_index]:
                    new_arr = arr[:]
                    new_arr[zero_index], new_arr[move] = new_arr[move], \
                                                           new_arr[zero_index]
                    new_s = ''.join(new_arr)
                    if new_s not in visited:
                        queue.append(new_s)

            step += 1

        return -1
```
