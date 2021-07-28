## 只出现一次的数字

在一个只有一个数字出现一次的列表中，找到这个数字。

O(N)且不开空间

```python
class Solution:
    def single_num(self, nums):
        s = 0
        for num in nums:
            s ^= num

        return num
```
