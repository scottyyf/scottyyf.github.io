# 最长回文子串

回文子串就是正反读都一样的字符串

可能是:

* xxxAxxx
* xxxAAxxx

```python
class Solution:
    def longest(self, s):
        res = ""
        for i in range(len(s)):
            tmp = self.get_longest(s, i, i)
            if len(tmp) > len(res):
                res = tmp

            tmp = self.get_longest(s, i, i+1)
            if len(tmp) > len(res):
                res = tmp

        return res


    def get_longest(self, s, l, r):
        while l >=0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1, r] # l+1是因为最后那个不成立的条件也被减去了1（left)
```
