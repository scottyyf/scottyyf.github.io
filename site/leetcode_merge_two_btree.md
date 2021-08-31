# 合并二叉树

dfs

* 结束条件
* 返回值
* 处理当前值
* 下探到下一层
* 清理环境

```python
class Solution:
    def merge_trees(self, t1, t2):
        # 下面这个也可以说是前序
        if not t1:
            return t2
        if not t2:
            return t1
        
        # 当前root层
        node = TreeNode(t1.val + t2.val)
        # 左子树为合并的左子树
        node.left = self.merge_trees(t1.left, t2.left)
        # 右子树为合并的右子树
        node.right = self.merge_trees(t1.right, t2.right)
        # 返回值
        return node
```


bfs

```python
class Solution:
    def merge_trees(self, t1, t2):
        # 单个tree， 直接返回，不需要合并
        if not t1：
            return t2
        if not t2:
            return t1

        # 合并tree为merged
        mereged = TreeNode(t1.val+t2.val)

        # 3个序列
        q = [merged]
        q1 = [t1]
        q2 = [t2]

        # 当有一个序列为空，则不需要进行合并了
        while q1 and q2:
            node = q.pop(0)
            node1 = q1.pop(0)
            node2 = q2.pop(0)

            left1, right1 = node1.left, node1.right
            left2, right2 = node1.right, node2.right

            # 合并左子树
            if left1 or left2:
                if left1 and left2:
                    left = TreeNode(left1.val + left2.val)
                    node.left = left
                    q.append(left)
                    q1.append(left1)
                    q2.append(left2)
                if left1:
                    node.left = left1

                if left2:
                    node.left = left2

            # 合并右子树
            if right1 or right2:
                if right1 and right2:
                    right = TreeNode(right1.val + right2.val)
                    node.right = right
                    q.append(right)
                    q1.append(right1)
                    q2.append(right2)
                if right1:
                    node.right = right1
                if right2:
                    node.right = right2
        # 返回值
        return merged
```
