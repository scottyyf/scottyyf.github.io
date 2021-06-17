# [最小基因变化](https://leetcode-cn.com/problems/minimum-genetic-mutation/)

要求： 

* 和单词接龙是一样的题

双向bfs
```python
class Solution:
    def minMutation(self, start: str, end: str, bank: list) -> int:
        if end not in bank:
            return -1

        begin_word = [start]
        end_word = [end]
        step = 0
        while begin_word:
            step += 1
            next_word = []
            for word in begin_word:
                for index in range(len(word)):
                    for c in ['A', 'C', 'G', 'T']:
                        if c == word[index]:
                            continue

                        new_word = word[:index] + c + word[index + 1:]
                        if new_word in end_word:
                            return step

                        if new_word in bank:
                            next_word.append(new_word)
                            bank.remove(new_word)

            begin_word = next_word
            if len(begin_word) > len(end_word):
                begin_word, end_word = end_word, begin_word

        return -1
```
