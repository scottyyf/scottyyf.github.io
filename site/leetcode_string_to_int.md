# [字符串转换整数](https://leetcode-cn.com/problems/string-to-integer-atoi/)

完全不考虑溢出问题，因为python3自动使用long类型

```python
class Solution:
    def str2int(self, s:str) -> int:
        s = list(s.lstrip())
        if not s:
            return 0

        sign = -1 if s[0] == '-' else 1
        if s[0] in ['-','+']:
            del s[0]

        ret = 0
        for i in s:
            if not i.isdigit():
                break

            ret = ret*10+int(i)

        reutrn max(-2**31, min(ret, 2**31-1))
```


和java一样的写法

```python
class Solution:
    def str2int(self, s: str) -> int:
        max_value, min_value = 2 ** 31 -1, -2 ** 31
        index, sign, total = 0, 1, 0
        while s[index] == ' ' and index < len(s):
            index += 1

        if index == len(s) - 1:
            return 0

        if s[index] in ['-', '+']:
            sign = -1 if s[index] == '-'
            index += 1

        while index < len(s):
            d = s[index]
            if not d.isdigit():
                break
            
            if max_value // 10 < total or (max_value // 10 == total and max_value % 10 < d):
                return max_value if sign == 1 else min_value

            total = 10 * total + d
            index += 1

       return total * sign
```
