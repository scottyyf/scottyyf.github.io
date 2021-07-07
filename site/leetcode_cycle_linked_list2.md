# [环形链表](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

要求：

* 找出环形所在的起始点

解法：

1. 暴力法：使用hash map存储遇到过的node，如果后续再遇到，那么就是环形所在的节点
```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        node_list, current_node = [], head
        while current_node:
            if current_node not in node_list:
                node_list.append(current_node)
                current_node = current_node.next
                continue
            return current_node

        return
```

2. 快慢指针。

假设经过时间t，两者相遇
* 快指针。那么他走的距离为2t
* 慢指针。走的距离为t

设直线有a个节点，环形中有b个节点。t时间相遇时，快指针走过的节点数为f，慢指针为s。则有

* f = 2t = a + x
* s = t = a + y
* f - s = t = nb
* f = 2nb, s = nb

nb + a 为环形起始点，那么 当前s慢指针在走a步一定会和在出发点走a步的人遇到，通过这个找到起始点

-----20210707

有 2t - t =  nS环，即t=ns。也就是说这个时间慢指针走了ns的距离

此时，再将慢指针走A步，那么会和从head出发的A步相遇。该相遇点，即为环形起始点。不懂就画图

以下这种方法，有2t + 1 -t = nS,所以在prev的时候，slow还需要再走一步
```python
class Solution:
    def detectCycle(self, head):
        """
        """
        if not head or not head.next:
            return None

        slow, fast = head, head.next
        if slow == fast:
            return slow

        while slow != fast:
            slow = slow.next

            if not fast.next or not fast.next.next:
                return None

            fast = fast.next.next
            if fast == slow:
                break

        # slow get together
        slow = slow.next
        prev = head
        while slow != prev:
            slow, prev = slow.next, prev.next

        return prev
```

* do while。这个要比上面的好看，由于slow和fast的出发点是一样的，所以不需要再给slow再加一步
```python
class Solution:
    def detectCycle(self, head):
        if not head:
            return 

        slow, fast, prev = head, head, head
        while True:
            if not fast.next or not fast.next.next:
                return None

            slow, fast = slow.next, fast.next.next
            if slow == fast:
                break

        while slow != prev:
            slow, prev = slow.next, prev.next

        return prev
```
