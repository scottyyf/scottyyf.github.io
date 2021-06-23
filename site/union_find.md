# 并查集

并查集： 用于查找两个事物之间是否存在联系，如两个人是否有关联关系（朋友的朋友）

* 并查集中p[i] = i 表示i个元素的parent是i自己，画图表示为，他就是这组关系中的头
* 并查集的合并（union），将一个集合并入另外一个集合，只需要将这组集合的头并入另外一个集合的头即可
* 并查集的路径压缩。在寻找当前节点的parent时，将该节点直接移动到parent的后面，减少查询的height

```python
class UnionFind:
    def __init__(self, n: int):
        self.p = [i for i in range(n)]

    def union(self, p: int, q: int):  # 合并操作
        p_root = self.parent(p)
        q_root = self.parent(q)
        if p_root != q_root:
            self.p[p_root] = q_root

    def parent(self, p: int):
        root = p
        while self.p[root] != root: # 查找当前集合的头节点
            root = self.p[root]

        while self.p[p] != p:  # 路径压缩，压缩当前节点及以上
            x = p
            p = self.p[p]
            self.p[x] = root
            
        return root
```
