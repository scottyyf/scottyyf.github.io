# 重塑矩阵

在MATLAB中，有一个非常有用的函数 reshape，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，以及两个正整数r和c，分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。

如果具有给定参数的reshape操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。

链接：https://leetcode-cn.com/problems/reshape-the-matrix

1. 二维变一维，然后再导向二维

```python
class Solution:
    def reshape(self, nums, r, c):
        row, col = len(nums), len(nums[0])

        if r * c != row * col:
            return mat

        new_list = [[0] * c for _ in range(r)]
        for x in range(row * col):
            new_list[x//c][x%c] = mat[x//col][x%col]  # 注意这里都是column

        return new_list
```
