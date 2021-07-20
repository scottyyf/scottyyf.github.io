# 字母异位词分组

输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]

输出: [["bat"],["nat","tan"],["ate","eat","tea"]]

```python
class Solution:
    def groupAnagrams(self, strs):
        data = {}
        for char in strs:
            key = sorted(char)
            data[key] = data.get(key, []) + [char] # 主要还是这句

        return list(data.values())
```
