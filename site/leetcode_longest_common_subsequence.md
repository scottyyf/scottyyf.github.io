# [最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

要求:

* 给出str1 和 str2,要求求出他们最长的公共子串

附： 这里我想到一个，str2是不是str1剔除一些字符串得到的子串。
这个可以用两个指针分别指向str1, str2的开头，然后逐步后移


dp方案，二维， O(mn)
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        rows, columns = len(text1), len(text2)
        dp = [[0] * (columns + 1) for _ in range(rows + 1)]

        for row in range(1, rows + 1):
            for column in range(1, columns + 1):
                if text2[column-1] == text1[row-1]:
                    dp[row][column] = dp[row - 1][column - 1] + 1
                else:
                    dp[row][column] = max(dp[row - 1][column],
                                          dp[row][column - 1])

        return dp[rows][columns]
```
