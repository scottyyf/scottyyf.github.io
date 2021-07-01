# [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

要求：

* 两个字符串，可以对他们增，删，替换字符 使两个字符相同。求这个操作的最小步数

BFS 和 DP

* dp

```python
class Solution:
    def edit_distance(self, words1: str, words2: str) -> int:
        dp = [[0] * (len(word2) + 1) for _ in range(len(word1)+1)]
        for i in range(1, len(words1)+1):
            dp[i][0] = i

        for j in range(1, len(words2)+1):
            dp[0][j] = j

        for i in range(1, len(words1)+1):
            for j in range(1, len(words2)+1):
                if words[i] == words[j]:
                    dp[i][j] = min(dp[i-1][j]+1, dp[i][j-1]+1, dp[i-1][j-1])
                else:
                    dp[i][j] = min(dp[i-1][j]+1, dp[i][j-1]+1, dp[i-1][j-1]+1)

        return dp[-1][-1]
```

* 单向bfs

```python
class Solution:
    def edit_distance(self, words1, words2):
        visited, queue = [], [(words1, words2)]
        step = 0
        while queue:
            for _ in range(len(queue)):
                w1, w2 = queue.pop(0)
                if (w1, w2) not in visited:
                    if w1 == w2:
                        return step
                    
                    visited.append((w1, w2))
                    while w1 and w2 and w1[0] == w2[0]:
                        w1, w2 = w1[1:], w2[1:]
                    
                    queue.append((w1[1:], w2))
                    queue.append((w1, w2[1:])
                    queue.append((w1[1:], w2[1:])

            step += 1       

        return step
```
