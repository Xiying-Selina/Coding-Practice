# Day 32+33休息

## 122. Best Time to Buy and Sell Stock II

[link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        # 贪心：每天收集正利润
        for i in range(1,len(prices)):
            profit += max(prices[i]-prices[i-1],0)
        return profit
```

## 55. Jump Game

[link](https://leetcode.com/problems/jump-game/description/)

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        # 贪心：每次跳最大跳跃步数，看能否覆盖终点
        cover = 0 # 记录覆盖
        if len(nums) == 1: return True # base case
        for i in range(len(nums)):
            if i<=cover:
                cover = max(cover, i+nums[i])
                if cover >=len(nums)-1: return True
        return False
```

## 45. Jump Game II

[link](https://leetcode.com/problems/jump-game-ii/description/)

````python
// ```python3
class Solution:
    def jump(self, nums: List[int]) -> int:
        curDistance = 0    # 当前覆盖的最远距离下标
        ans = 0    # 记录走的最大步数
        nextDistance = 0   # 下一步覆盖的最远距离下标
        # 控制移动下标i只移动到len(nums)- 2的位置，
        # 所以移动下标只要遇到当前覆盖最远距离的下标，直接步数加一
        for i in range(len(nums)-1):
            nextDistance = max(nums[i] + i, nextDistance) #更新下一步覆盖的最远距离下标
            if (i == curDistance):            #遇到当前覆盖的最远距离下标
                curDistance = nextDistance    #更新当前覆盖的最远距离下标
                ans+=1
        return ans
```
````
