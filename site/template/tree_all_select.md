# 左，中，后序遍历

遍历的顺序是指root的位置

node:

```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
```

前序遍历

```python
def preorder(root: Node):
    if root:
        self.traverse_path.append(root.val)
        self.preorder(root.left)
        self.preorder(root.right)
```

中序遍历

```python
def inorder(root: Node):
    if root:
        self.inorder(root.left)
        self.traverse_path.append(root.val)
        self.inorder(root.right)
```

后序遍历

```python
def postorder(root: Node):
    if root:
        self.postorder(root.left)
        self.postorder(root.right)
        self.traverse_path.append(root.val)
```

二叉搜索树：left  < root < right且满足左子树 < root < 右子树

* 搜索： logn
* 插入： logn
* 创建： 依次插入空树
* 删除： 找到被删除节点，并将被删除节点的右子树最小节点替换掉被删除节点
