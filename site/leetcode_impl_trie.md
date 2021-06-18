# [实现Trie](https://leetcode-cn.com/problems/implement-trie-prefix-tree/submissions/)

要求：

* 实现字典树

```pyhton
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        self.end_mark = '#'

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.root
        for c in word:
            node = node.setdefault(c, {})

        node[self.end_mark] = self.end_mark

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.root
        for c in word:
            if c not in node:
                return False

            node = node[c]

        return self.end_mark in node

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given
        prefix.
        """
        node = self.root
        for c in prefix:
            if c not in node:
                return False

            node = node[c]

        return True
```
