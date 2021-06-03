# 硬币组合

硬币有[2,5,7]足量，求拼凑出27需要的最小硬币数量

dp算法可求：

* 计数问题，how many
* 最值问题，最大值最小值
* 存在性问题，is there

这个题是最值问题：

1. 原则来说，dp问题和递归问题没有本质区别，只是中间结果被存储起来，不需要多次计算
2. dp的问题，一般会转化为for循环解答，而不用递归那套。这个是打比赛时，为了寻求最优解

O(mn)
```python
def coin_change(A: list, M: int) -> int:
    # 递归结束条件
    dp = {0: 0}
    # 递归下探时的逻辑
    for num in range(1, M + 1):
        dp[num] = sys.maxsize
        for coin in A:
            if num >= coin and dp[num - coin] != sys.maxsize:
                dp[num] = min(dp[num - coin] + 1, dp[num])

    if dp[M] == sys.maxsize:
        return -1

    return dp[M]
```

机器人从左上角到右下角的路径数量。这个是数量问题

路径唯一，求可到达的路径数量
```python
def go_to_end(m: int, n: int):
    dp = [[0 for _ in range(n)] for _ in range(m)]
    for row in range(m):
        for column in range(n):
            if row == 0 or column == 0:
                dp[row][column] = 1

            else:
                dp[row][column] = dp[row - 1][column] + dp[row][column - 1]

    return dp[m - 1][n - 1]
```

存在性问题。 这个还能用贪心算法

青蛙跳石板问题。x轴0到n-1,青蛙从0想跳到n-1,青蛙在i块石头时，最多可向右跳距离Ai。
问：青蛙能否跳到n-1的石头上面

1. 确定状态： 最后一步到ak，则需要ak + k >=n-1，青蛙能从ak跳到n-1；那么青蛙能否到达ak，所以子问题为f(x) 能否跳到x
2. 转移方程： f[j] = 对0-j内 F[i]为真 且 i+ai >= j
3. 初始条件和边界： f[0]=True
4. 计算顺序。0到n-1

时间复杂度 O(n^2)
```python
def can_jump(A: list):
    dp = {0: True}
    for stone in range(1, len(A)):
        dp[stone] = False
        for step in range(stone):
            if dp[step] and step + A[step] >= stone:
                dp[stone] = True
                break

    return dp[len(A) - 1]
```
