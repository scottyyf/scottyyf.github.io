# 选择餐馆

从美团爬取数据后，进行过滤

| ID | rating | flavor | price | distance |
| -- | -- | -- | -- | -- |

filter过滤条件

| flavor | maxprice | maxdistance |
| -- | -- | -- |

```python
from operator import itemgetter
class Solution:
    def filter_res(self, restaurants: list, filters: list) -> list:
        if filters[0] == 1:
            ret = [x for x in restaurants if x[2] == filters[0] and x[3] <= filters[1] and x[4] <= filters[2]]
        else:
            ret = [x for x in restaurants if x[3] <= filters[1] and x[4] <= filters[2]]

        ret.sort(key=itemgetter(1, 0), reverse=True)
        return [x[0] for x in ret]
```
