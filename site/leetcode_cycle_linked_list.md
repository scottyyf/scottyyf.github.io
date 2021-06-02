# [环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

要求：

* 找出当前是否有环
* 更进一步的，找出哪个node为环的起始点

是否有环

解法：

1. 暴力解法：存储所有遇到的node，判断下一个node是否已经在存储的node中。

2. do-while 循环，将两个指针初始点放一起，然后追赶
```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head:
            return False

        slow, fast = head, head
        while True:
            if not fast.next or not fast.next.next:
                return False

            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
```

3. while loop循环。由于while条件，所以slow和fast不能指向同一个node
```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head or not head.next:
            return False

        slow, fast = head, head.next
        # 单节点环
        if slow == fast:
            return True
        
        while slow != fast:
            slow = slow.next
            if not fast.next or not fast.next.next:
                return False

            fast = fast.next.next
            if slow == fast:
                return True
```
