# 数据流查询

某公司开发设计了一个名为 X 的数据流管理系统，用以处理对数据流的查询。用户可以在 X 中进行注册查询，X 将保持在不断变化的数据上执行查询，并且按照用户所需要的频率返回结果。

优先队列

```python
from query import PriorityQueue


class QueryObject:
    def __init__(self, query_id, start_time, period):
        self.query_id = query_id
        self.start_time = start_time
        self.period = period

    def __call__(self, *args, **kwargs):
        return self.start_time, self.query_id, self.period


class Solution:
    def findTopQuery(self, orders, k):
        ret = []
        a_queue = PriorityQueue()

        for order in orders:
            a_queue.put(QueryObject(*order))

        for _ in range(k):
            first_q = a_queue.get()
            ret.append(first_q[1])
            a_queue.put(QueryObject(first_q[1], first_q[0] + first_q[2], first_q[2]))

        return ret
```
