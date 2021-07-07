# [K个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

递归.这个和翻转2个节点类似。

```python
class Solution:
    def reverse_group(self, head: LinkedNode, k: int):
        tail = head
        for i in range(k):
            # 这里只需要k个节点，这个for循环后将会有k+1个节点，所以先判断再下一个
            is not tail:
                reutrn head

             tail = tail.next

        new_node = self.reverse(head, tail)
        # 这里的tail已经是第k+1开始的节点了
        head.next = self.reverse_group(tail, k) 
        return new_node

    def reverse(self, head, tail):
        # 翻转linknode
        pre = None
        while prev != tail: # 这里不是head != tail，因为tail是k+1的节点，不是k节点
            nex = head.next
            head.next = pre
            pre = head
            head = nex

        return pre
```

这里就不用逻辑写法了，太麻烦了。用递归简单明了
