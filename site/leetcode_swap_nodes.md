# [两两交换链表节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

要求：

* 1 -> 2 -> 3 -> 4 TO 2 -> 1 -> 4 -> 3

解法：

递归：

1. 结束条件。head为空或者head的next为空，无法继续交换
2. 当前层处理逻辑。因为结果需要返回新的链表头，根据先递后归，那么最后返回的是初始head时的返回值。这里需要返回head.next
3. 下探到下一层。下一层的返回值将作为head.next指针，也就是1 -> 下一层的返回值
4. 当前层逻辑指针处理。因为第2步骤处理这个逻辑将导致第3步骤死循环，所以这个步骤放在3步骤后处理。即 ret.next = head
5. 清理状态值

```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        ret = head.next
        head.next = self.swapPairs(head.next.next)
        ret.next = head
        return ret
```
