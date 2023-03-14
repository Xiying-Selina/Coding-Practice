# Day 38: Fibonacci

## 509. Fibonacci Number

[link](https://leetcode.com/problems/fibonacci-number/description/)

````python
// ```python3
class Solution:
    def fib(self, n: int) -> int:
        # corner case
        if n==0: return 0
        # 创建 dp table 
        dp = [0]*(n+1)
        # 初始化 dp 数组
        dp[0] = 0
        dp[1] = 1

        # 遍历顺序: 由前向后。因为后面要用到前面的状态
        for i in range(2, n + 1):

            # 确定递归公式/状态转移公式
            dp[i] = dp[i - 1] + dp[i - 2]
        
        # 返回答案
        return dp[n]
```
````

## 70. Climbing Stairs

[link](https://leetcode.com/problems/climbing-stairs/description/)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # dp[i]: 达到第i阶所有dp[i]种方法
        # dp[i] = dp[i-1]+dp[i-2]
        if n==0: return 0
        dp = [0]*(n+1)
        dp[0]=1
        dp[1]=1
        for i in range(2,n+1):
            dp[i]=dp[i-1]+dp[i-2]
        return dp[n]
```

## 746. Min Cost Climbing Stairs

[link](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

````python
// ```python3
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        # dp[i]: 到i阶梯所需要最小花费
        dp = [0]*(len(cost)+1)
        dp[0], dp[1] = 0, 0
        for i in range(2, len(cost)+1):
            dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2])
        return dp[len(cost)]
```
````
