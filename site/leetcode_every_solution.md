# LRU缓存模拟
要求：

* 访问和新增的时间复杂度为O(1)
* 对于链表来说，新增和删除都是O(1),但是访问是O(n)
* 对于列表来说，新增和删除是O(n),访问是O(1)
* 为了能灵活新增与删除，采用双链表
* 为了O(1)访问，额外开个空间，存储已经存在的key

```python
class LinkNode:
    def __init__(self, key=None, value=None):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None


class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.size = 0

        self.head = LinkNode()
        self.tail = LinkNode()
        self.head.next = self.tail
        self.tail.prev = self.head

        self.exist_node = {}

    def get(self, key: int) -> int:
        if not key in self.exist_node:
            return -1

        node = self.exist_node[key]
        self.add_to_head(node)
        return node.value

    def put(self, key: int, value: int) -> None:
        if key in self.exist_node:
            node = self.exist_node[key]
            node.value = value
            self.add_to_head(node)

        else:
            node = LinkNode(key, value)
            self.move_to_head(node)
            self.exist_node[key] = node
            self.size += 1
            if self.size > self.capacity:
                node = self.remove_tail_node()
                self.exist_node.pop(node.key)
                self.size -= 1

    def remove_tail_node(self):
        tail_node = self.tail.prev
        self.remove_node(tail_node)
        return tail_node

    def add_to_head(self, node: LinkNode):
        self.remove_node(node)
        self.move_to_head(node)

    def remove_node(self, node: LinkNode):
        node.prev.next = node.next
        node.next.prev = node.prev

    def move_to_head(self, node: LinkNode):
        node.prev = self.head
        node.next = self.head.next

        self.head.next.prev = node
        self.head.next = node
```
