# Day 34

## 1005. Maximize Sum Of Array After K Negations

[link](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/description/)

```python
class Solution:
    def largestSumAfterKNegations(self, nums: List[int], k: int) -> int:
        # 让绝对值大的负数变为正数，让0或最小正数变余下次数 -> 错误
        # 会出现 nums=[-8,3,-5,-3,-5,-2],k=6 outpuut=20,但实际解为22
        # 应该按照绝对值对nums排序，从前向后遍历，遇到负数将其变为正数，同时K--
        # 如果K还大于0，那么反复转变数值最小的元素，将K用完
        nums = sorted(nums,key=abs,reverse=True) # 将nums按绝对值从大到小排列
        # nums=[-8,-5,-5,-3,3,-2] k=6
        for i in range(len(nums)):
            if k>0 and nums[i]<0:
                nums[i]=-nums[i]
                k-=1
        #  nums=[8,5,5,3,3,2] k=1
        if k>0:
            nums[-1] *= (-1)**k
        return sum(nums)
        


```

## 134. Gas Station

[link](https://leetcode.com/problems/gas-station/description/)

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        start = 0 # 记录起始位置
        # 每个加油站的剩余量rest[i]为gas[i] - cost[i]
        curSum = 0 # i从0开始累加rest[i]，和记为curSum
        totalSum = 0 # 记录当前累加rest[i]
        # 局部最优：totalSum和curSum一旦小于0，起始位置至少要是i+1，因为从i之前开始一定不行。
        # 全局最优：找到可以跑一圈的起始位置
        for i in range(len(gas)):
            curSum += gas[i] - cost[i]
            totalSum += gas[i] - cost[i]
            # 一旦curSum小于零，说明[0, i]区间都不能作为起始位置，
            # 因为这个区间选择任何一个位置作为起点，到i这里都会断油，
            # 那么起始位置从i+1算起，再从0计算curSum。
            if curSum < 0:
                curSum = 0
                start = i + 1
        if totalSum <0: return -1
        return start
        
```

## 135. Candy

[link](https://leetcode.com/problems/candy/description/)

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        # 从前向后遍历:只比较右边孩子评分比左边大的情况
        # 局部最优：只要右边评分比左边大，右边的孩子就多一个糖果，
        # 全局最优：相邻的孩子中，评分高的右孩子获得比左边孩子更多的糖果.
        candies = [1]*len(ratings)
        for i in range(1,len(ratings)):
            if ratings[i]>ratings[i-1]:
                candies[i] = candies[i-1]+1
        # 从后向前遍历:只比较左边孩子评分比右边大的情况
        for j in range(len(ratings)-2, -1,-1):
            if ratings[j]>ratings[j+1]:
                candies[j] = max(candies[j+1]+1,candies[j])
        return sum(candies)
```
