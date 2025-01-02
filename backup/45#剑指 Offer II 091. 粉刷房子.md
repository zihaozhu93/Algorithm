# 剑指 Offer II 091. 粉刷房子

[剑指 Offer II 091. 粉刷房子](https://leetcode.cn/problems/JEj789)

假如有一排房子，共 n 个，每个房子可以被粉刷成红色、蓝色或者绿色这三种颜色中的一种，你需要粉刷所有的房子并且使其相邻的两个房子颜色不能相同。

当然，因为市场上不同颜色油漆的价格不同，所以房子粉刷成不同颜色的花费成本也是不同的。每个房子粉刷成不同颜色的花费是以一个 n x 3 的正整数矩阵 costs 来表示的。

例如，costs[0][0] 表示第 0 号房子粉刷成红色的成本花费；costs[1][2] 表示第 1 号房子粉刷成绿色的花费，以此类推。

请计算出粉刷完所有房子最少的花费成本。

> 动态规划方程；使用二维 dp[i][j] 表示粉刷到第 i 个房子且颜色为 j 时的最小花费。
> 初始化 dp[0][j] 为 costs[0][j]，即第一个房子的花费。
> 从第 1 个房子开始，计算每个房子的最小花费。对于每个房子，可以选择三种颜色中的一种，并且需要确保相邻房子的颜色不同。
> 最终结果是 dp[n-1][0]、dp[n-1][1] 和 dp[n-1][2] 中的最小值，即粉刷完所有房子的最小花费。

```
from typing import List

class Solution:
    def minCost(self, costs: List[List[int]]) -> int:
        if not costs:
            return 0
        
        n = len(costs)
        dp = [[0] * 3 for _ in range(n)]
        
        # 初始化第一个房子的花费
        dp[0][0] = costs[0][0]
        dp[0][1] = costs[0][1]
        dp[0][2] = costs[0][2]
        
        # 计算每个房子的最小花费
        for i in range(1, n):
            dp[i][0] = min(dp[i-1][1], dp[i-1][2]) + costs[i][0]
            dp[i][1] = min(dp[i-1][0], dp[i-1][2]) + costs[i][1]
            dp[i][2] = min(dp[i-1][0], dp[i-1][1]) + costs[i][2]
        
        # 返回最后一个房子的最小花费
        return min(dp[-1][0], dp[-1][1], dp[-1][2])

# 示例用法
solution = Solution()
costs = [[17, 2, 17], [16, 16, 5], [14, 3, 19]]
print(solution.minCost(costs))  # 输出 10
```

---

* Link: https://github.com/zihaozhu93/Algorithm/issues/45
* Labels: `dp`
* Creation Date: 2025-01-02T07:15:48Z
