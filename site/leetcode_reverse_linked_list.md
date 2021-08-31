# [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

要求：

* 将链表反转

附： 链表的题目，一般都要画图作答

解法：

暴力法：链表无法使用for进行遍历，如果可以遍历，那么可以很好的解答。这里借助列表,一般不用这种方法，因为空间消耗过大
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        curr = head
        ret = []
        while curr is not None:
            ret.append(curr)
            curr = curr.next

        prev = None
        for node in ret:
            node.next = prev
            prev = node

        return prev
```

迭代法：(画图过程中出现解法2021/08/06)从前往后一一变更指针方向，为了获取下一个node，这里需要额外的空间存在这个值以便进行遍历
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev, current = None, head
        while current:
            next = current.next
            current.next = prev
            prev = current
            current = next

        return prev
```

递归法：先递再归，完成顺序是后面的先完成

* 结束条件
* 当前层处理逻辑（因为这里是两个节点的关系，所以当前层没有处理逻辑）
* 下探到下一层。到下一层时，这里需要将指针指回去，并且将上一层的指针置为空
* 清理状态值
* 因为这里需要返回新的头，所以将最后面得到的new node 一层一层的往外面抛
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        # 不需要在当前层做任何操作， 所以无
        next_node = self.reverseList(head.next) # 这里是到下一层，没想出下一层要干嘛，所以就返回个node
        
        head.next.next = head # 这里才是实际的reverse操作
        head.next = None # 这个地方的none不会出问题的原因是，head.next = none 是从队尾开始复制的

        return next_node # 这里返回的是最后一个满足条件的值，也就是新的表头。理解递归的画图
```
