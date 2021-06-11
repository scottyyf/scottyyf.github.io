# []()

要求：

* 根据数据产生不同的字符组合

递归
```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        letters = {
            '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno',
            '7': 'pqrs', '8': 'tuv', '9': 'wxyz',
            }

        ret = []
        self._combinate_letter('', digits, 0, ret, letters)
        return ret

    def _combinate_letter(self, tmp_str: str, digits: str, current_level: int,
                          ret: list, letters: dict):
        if current_level == len(digits):
            ret.append(tmp_str)
            return

        content = letters.get(digits[current_level])
        for chart in content:
            self._combinate_letter(tmp_str + chart, digits, current_level + 1,
                                   ret, letters)
```
