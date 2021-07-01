# [翻转字符串中的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

要求：

* the sky is 到 is shy the

O(1)的空间复杂度

由于string是immutable,所以不能使用strip，reverse等内定义的函数。因为他们会再创一个对应string

```python
class Solution:
    def reverse_words(self, s: str) -> str:
        arr = list(s)
        if ''.join(arr).isspace() or not arr:
            return ''

        self.reverse_string(arr, 0, len(arr)-1)
        self.reverse_word(arr)
        words = self.strip_sides(arr)
        return self.strip_space(words)

    def reverse_string(self, arr, left, right):
        while left < right:
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1

    def reverse_word(self, arr):
        left, right = 0, 0
        while right < len(arr):
            while right < len(arr) and not arr[right].isspace():
                right += 1

            self.reverse_string(arr, left, right-1)
            right += 1
            left = right

    def strip_sides(self, arr):
        left, right = 0, len(arr)-1
        while left < right and arr[left].isspace():
            left += 1

        while left < right and arr[right].isspace():
            right -= 1

        return arr[left: right+1]

    def strip_space(self, word):
        s = word[0]

        for i in word:
            if i.isspace() and s[-1].isspace():
                continue

            s += i

        return s
```
