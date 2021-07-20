# 中序遍历 

这个还是要脑子中有图

输出中序遍历的结果

```python
class Solution:
    def inorder_traversal(root):
        ret = []
        self.inorder(root, ret)
        return ret

    def inorder(root, ret):
        if root:
            self.inorder(root.left)
            ret.append(root.val)
            self.inorder(root.right)
```

# N叉树的层序遍历 BFS

```python
class Solution:
    def levelOrder(self, root: Node):
        queue, ret = [root], []
        if not root:
            return ret

        while queue:
            level_ret = []
            for _ in range(len(queue)):
                node = queue.pop(0)
                level_ret.append(node.val)
                queue.extend(node.children)

            ret.append(level_ret)

        return ret
```
