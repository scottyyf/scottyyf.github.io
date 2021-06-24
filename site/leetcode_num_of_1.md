# [位运算](https://leetcode-cn.com/problems/number-of-1-bits/)

要求：

* 给出一个二进制的整数，求里面1的个数

位运算1： 每次剔除最低位的1
```python
class Solution:
    def hammingWeight(self, n:int)->int:
        count = 0
        while n != 0:
            n = n & (n-1)
            count += 1
        return count
```

位运算2： 第i位为1时与n的与不为0,则说明该位置为1
```python
class Solution:
    def hammingWeight(self, n:int) -> int:
        count = 0
        for i in range(32):
            if n & (1<<i):
                count += 1

        return count
```
