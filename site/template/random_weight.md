# 加权随机

```python
from array import array
from bisect import bisect
from collections import defaultdict


class weightObj:
    def __init__(self, weight, obj):
        self.weight, self.obj = weight, obj


class weightRandom:
    def __init__(self):
        self._total_weight = 0
        self._weight = array('d')
        self._objs = []

    def add_obj(self, weight, obj):
        self._total_weight += weight
        self._weight.append(self._total_weight)
        self._objs.append(weightObj(weight, obj))

    def get_object(self):
        index = bisect(self._weight, random() * self._total_weight)
        return self._objs[index].obj

    def exclusive_get(self, count):
        ret = []
        tmp_total, tmp_objs, tmp_weight = self._total_weight, self._objs[:], deepcopy(self._weight)
        for _ in range(count):
            index = bisect(tmp_weight, random() * tmp_total)
            try:
                curr_obj = tmp_objs.pop(index)
                tmp_weight.pop(index)
            except Exception:
                return ret

            else:
                ret.append(curr_obj.obj)
                tmp_total -= curr_obj.weight
        return ret


if __name__ == '__main__':
    fc = weightRandom()
    for w, o in [(1, 'a'), (2,'b'), (5,'c')]:
        fc.add_obj(w,o)

    dd = defaultdict(int)
    for _ in range(1000):
        obj = fc.get_object()
        dd[obj] += 1

    print(dict(dd))
```
