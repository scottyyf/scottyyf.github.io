# [2的幂](https://leetcode-cn.com/problems/power-of-two/)

要求：

* 给你一个整数 n，请你判断该整数是否是 2 的幂次方。如果是，返回 true ；否则，返回 false 。

x & -x 得到最低位的1, 2的幂是指整个二进制中只有一个1
```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        return n > 0 and n & -n == n
```

x & (x - 1) 清零最低位的1
```python
class Solution:
    def isPowerOfTwo(self, n:int) -> bool:
        return n > 0 and n & (n - 1) == 0
```
