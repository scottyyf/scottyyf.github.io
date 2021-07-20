# 两个有序数组合并一个有序数组

```python
ret = []
left， right = l1.head, l2.head
while left and right:
    if left.val < right.val:
        ret.append(left）
        left.pop(0)
    else:
        ret.append(right)
        right.pop(0)

while left:
    ret.append(left)
    left.pop(0)

while right:
    ret.append(right)
    right.pop(0)
```
