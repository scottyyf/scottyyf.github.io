# 填充每个节点下一个右侧节点指正

这个是层序遍历， 这个用BFS，且在while中用到了for。下面看具体

https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/

```python
class Solution:
    def connect(self, root):    
        if not root:
            return root

        queue = [root]
        while queue:
            size = len(queue)
            for i in range(size):
                node = queue.pop(0)
                if i < size - 1:
                    node.next = queue[0]
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return root
```
