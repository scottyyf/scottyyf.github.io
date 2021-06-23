# [岛屿问题](https://leetcode-cn.com/problems/number-of-islands/)

要求：
```text
# 给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。 
# 
#  岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。 
# 
#  此外，你可以假设该网格的四条边均被水包围。 
# 
#  
# 
#  示例 1： 
# 
#  
# 输入：grid = [
#   ["1","1","1","1","0"],
#   ["1","1","0","1","0"],
#   ["1","1","0","0","0"],
#   ["0","0","0","0","0"]
# ]
# 输出：1
```


* 网格问题：mxn的网格问题，岛屿问题就是典型的该问题。这类问题涉及求岛屿数量，岛屿面积，岛屿周长等，这都可以通过dfs遍历来解决
* 树的dfs代码结构
```python
def dfs(root):
    if root is None:
        return

    process_current_node()
   
    dfs(root.left)
    dfs(root.right)

    clear_state()    
```

* 网格dfs
```python
def dfs(grid, row, col):
    if not inside_area(grid, row, col):
        return

    if grid[row][col] != '1':
        return

    # visited
    grid[row][col] = 2

    # strip down
    # 这个地方，我也看到过别人用for循环做的，但是这样更直白
    dfs(grid, row - 1, col)
    dfs(grid, row + 1, col)
    dfs(grid, row, col - 1)
    dfs(grid, row, col + 1)
```

以下是岛屿数量代码dfs
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        count = 0
        if not grid or not len(grid[0]):
            return count

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == '1':
                    count += 1
                    self.dfs(grid, row, col)

        return count

    def dfs(self, grid, row, col):
        if row < 0 or row >= len(grid) or \
                col < 0 or col >= len(grid[0]):
            return

        if grid[row][col] != '1':
            return

        grid[row][col] = '2'
        self.dfs(grid, row + 1, col)
        self.dfs(grid, row - 1, col)
        self.dfs(grid, row, col - 1)
        self.dfs(grid, row, col + 1)
```

求最大岛屿的面积
```python
class Solution:
    def maxAreaOfIsland(self, grid: list):
        ret = 0
        if not grid or not len(grid[0]):
            return ret

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == '1':
                    tmp_ret = self.dfs(grid, row, col)
                    ret = max(ret, tmp_ret)

        return ret

    def dfs(grid, row, col):
        if row < 0 or row >= len(grid) or \
                col < 0 or col >= len(grid[0]):
            return 0

        if grid[row][col] != '1':
            return 0

        grid[row][col] = '2'

        return 1 + self.dfs(grid, row-1, col) + \
                self.dfs(grid, row+1, col) + \
                self.dfs(grid, row, col-1) + \
                self.dfs(grid, row, col+1)
```


岛屿的周长，方格中只有一个岛屿，求周长。岛屿周边有海的 +1,另外岛屿靠近岸边的+1
```python
class Solution:
    def island_perimeter(self, grid: list) -> int:
        perimeter = 0
        if not grid or not grid[0]:
            return perimeter

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col]:
                    ret = self.dfs(grid, row, col)

        return ret

    def dfs(self, grid, row, col):
        if not in_area(row, col, grid):
            return 1

        if grid[row][col] == '0':
            return 1

        if grid[row][col] != '1':
            return 0

        grid[row][col] = '2'
        return self.dfs(grid, row - 1, col) + \
                self.dfs(grid, row + 1, col) + \
                self.dfs(grid, row, col - 1) + \
                self.dfs(grid, row, col + 1)
```
