# [单词搜索2](https://leetcode-cn.com/problems/word-search-ii/)

要求：

* 给出一组单词列表
* 给出一个mxm的矩阵，里面放字符
* 在矩阵中可上下左右，查询所有可拼装的单词列表

需要留意返回的结果中需要去重，而且dfs这些需要进行剪枝
```python
class Trie:
    def __init__(self):
        self.root = {}
        self.end_mark = '#'

    def insert(self, word: str):
        node = self.root
        for c in word:
            node = node.setdefault(c, {})

        node[self.end_mark] = self.end_mark

    def search(self, word):
        node = self.root
        for c in word:
            if c not in node:
                return False

            node = node[c]

        return self.end_mark in node

    def start_with(self, word):
        node = self.root
        for c in word:
            if c not in node:
                return False

            node = node[c]

        return True


class Solution:
    def findWords(self, board: list, words: list) -> list:
        result = set()
        if not board or not board[0] or not words:
            return list(result)

        self.trie = Trie()
        for word in words:
            self.trie.insert(word)

        root = self.trie.root
        for row in range(len(board)):
            for col in range(len(board[0])):
                if board[row][col] in self.trie.root:
                    self.dfs(board, result, row, col, '', root)

        return list(result)

    def dfs(self, board: list, result: set, row: int, col: int, res: str,
            root: dict):
        if self.trie.end_mark in root:
            result.add(res)

        if row < 0 or row >= len(board) or \
                col < 0 or col >= len(board[0]) or \
                board[row][col] == '@':
            return

        tmp, board[row][col] = board[row][col], '@'
        root = root.get(tmp)
        if not root:
            board[row][col] = tmp
            return

        self.dfs(board, result, row - 1, col, res + tmp, root)
        self.dfs(board, result, row + 1, col, res + tmp, root)
        self.dfs(board, result, row, col - 1, res + tmp, root)
        self.dfs(board, result, row, col + 1, res + tmp, root)
        board[row][col] = tmp


if __name__ == '__main__':
    board = [["o", "a", "a", "n"], ["e", "t", "a", "e"], ["i", "h", "k", "r"],
             ["i", "f", "l", "v"]]
    words = ["oath", "pea", "eat", "rain"]
    ret = Solution().findWords(board, words)
    print(ret)
# leetcode submit region end(Prohibit modification and deletion)
```


下面这个应该是更符合编程时的思想。实现trie, trie_node, 具体逻辑业务的分离。对于trie，实现了类型链表的东西.需要说明的是，node=self.root这句是引用，所以后面的is_end的值会被改变
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str):
        node = self.root
        for w in word:
            node = node.children.setdefault(w, TrieNode())

        node.is_end = True

    def search(self, word):
        node = self.root
        for w in word:
            if w not in node:
                return False

            node = node.children[w]

        return node.is_end

    def start_with(self, word):
        node = self.root
        for w in word:
            if w not in node:
                return False

            node = node.children[w]

        return True


class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        self.result = set()
        if not board or not board[0]:
            return list(self.result)

        trie = Trie()
        for word in words:
            trie.insert(word)

        node = trie.root
        row, column = len(board), len(board[0])
        for i in range(row):
            for j in range(column):
                if board[i][j] in trie.root.children:  # start
                    self.dfs(board, i, j, '', node)

        return list(self.result)

    def dfs(self, board: List[List[str]], i, j, curr_word, node: TrieNode):
        if node.is_end:
            self.result.add(curr_word)
            node.is_end = False

        if i < 0 or i >= len(board) or \
            j < 0 or j >= len(board[0]) or \
            board[i][j] =='@':
            return

        tmp, board[i][j] = board[i][j], '#'
        node = node.children.get(tmp)
        if not node:
            board[i][j] = tmp
            return

        self.dfs(board, i - 1, j, curr_word + tmp, node)
        self.dfs(board, i + 1, j, curr_word + tmp, node)
        self.dfs(board, i, j - 1, curr_word + tmp, node)
        self.dfs(board, i, j + 1, curr_word + tmp, node)
        board[i][j] = tmp
```
