# Lru cache
O(1)实现

* get(key) 获取并放到首
* put(key, value) 增加并放到首

```python
class LinkedList:
    def __init__(self, key=None, val=None):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None


class LruCache:
    def __init__(self, capacity):
        self.data = {}
        self.head = LinkedList()
        self.tail = LinkedList()
        self.head.next = self.tail
        self.tail.prev = self.head

        self.capacity = capacity
        self.size = 0

    def get(self, key):
        if key not in self.data:
            return -1

        node = self.data.get(key)
        self.move_to_head(node)
        return node.val

    def put(self, key, value):
        if key in self.data:
            node = self.data.get(key)
            node.val = value
            self.move_to_head(node)

        else:
            node = LinkedList(key, value)
            self.add_to_head(node)
            self.data[key] = node
            self.size += 1
            if self.size > self.capacity:
                self.size -= 1
                node = self.remove_tail_node()
                self.data.pop(node.key, None)

    def remove_tail_node(self):
        # no node to remove
        if self.head.next == self.tail:
            return LinkedList()

        tail = self.tail.prev
        self.remove_node(tail)
        return tail
        
    def move_to_head(self, node):
        self.remove_node(node)
        self.add_to_head(node)

    def remove_node(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
        node.prev = None
        node.next = None

    def add_to_head(self, node):
        # 这里先添加node的指向，再改变已有node的指向
        node.prev = self.head
        node.next = self.head.next

        self.head.next.prev = node
        self.head.next = node
```
