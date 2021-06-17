# [单词接龙](https://leetcode-cn.com/problems/word-ladder/)

要求：

* 给出初始和目标单词，每次只允许变更一个字符，根据给出的wordlist，求出最短路劲

查询目标A到目标B的最小距离，和找人一样，在每一层都遍历每个熟悉的人。所以这里用BFS

BFS。对于每个单词，通过每个字符用a-z替换，如果替换出来的字符在wordlist中，
那么这些单词将作为下一层的beginword；每一层完成后，step加1
```python
class Solution:
     def _ladderLength(self, beginWord: str, endWord: str,
                       wordList: list) -> int:
         if endWord not in wordList:
             return 0

         if beginWord in wordList:
             wordList.remove(beginWord)

         return self.bfs(beginWord, endWord, wordList)

     def bfs(self, beginword, endword, wordlist: list):
         queue = [beginword]
         visited = set()
         step = 1
         while queue:
             nodes_length = len(queue)
             step += 1
             for _ in range(nodes_length):
                 node = queue.pop(0)

                 for i in range(len(node)):
                     for c in string.ascii_lowercase:
                         if c == node[i]:
                             continue

                         next_word = node[:i] + c + node[i + 1:]
                         if next_word in wordlist:
                             if next_word == endword:
                                 return step

                             if next_word not in visited:
                                 visited.add(next_word)
                                 queue.append(next_word)

         return 0

```

由于BFS中，越往下探，那么bfs的数越大，所以这里用双向BFS减少次数。
一端做过的路径，一旦在另一端路径中，那么就说明最开始的相遇，路径最短
```python
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: list) -> int:
        if endWord not in wordList:
            return 0

        begin_word, end_word, word_list = [beginWord], [endWord], set(wordList)
        step = 1

        while begin_word:
            step += 1
            next_word = []
            for word in begin_word:
                for index in range(len(word)):
                    for c in string.ascii_lowercase:
                        if c == word[index]:
                            continue

                        new_word = word[:index] + c + word[index + 1:]
                        if new_word in end_word:
                            return step

                        if new_word in word_list:
                            next_word.append(new_word)
                            word_list.remove(new_word)

            begin_word = next_word
            if len(begin_word) > len(end_word):
                begin_word, end_word = end_word, begin_word

        return 0
```
