# Day 31

## 455.  Assign Cookies

[link](https://leetcode.com/problems/assign-cookies/description/)

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        # 思路一：优先小胃口
        # 先遍历饼干，再遍历胃口
        g.sort()
        s.sort()
        res = 0 # 记录吃饼干的小孩个数，也是小孩的index
        for i in range(len(s)):
            if res<len(g) and s[i]>=g[res]:
                # 如果胃口被满足，到下一个小孩
                res+=1
        return res
```

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        # 思路二：优先大胃口
        # 先遍历胃口，再遍历饼干
        g.sort()
        s.sort()
        res, index = 0, len(s)-1 # 记录吃饼干的小孩个数，index记录饼干的index
        for i in range(len(g)-1,-1,-1):
            if index>=0 and s[index]>=g[i]:
                # 如果胃口被满足，到下一个小孩
                res+=1
                index-=1
        return res
```

## 376. Wiggle Subsequence

[link](https://leetcode.com/problems/wiggle-subsequence/description/)

```python
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
        # 局部最优：删除单调坡度上的元素
        if len(nums)==1: return 1
        prediff, curdiff, res = 0, 0, 1
        for i in range(len(nums)-1):
            curdiff = nums[i+1] - nums[i]
            if (prediff >=0 and curdiff < 0) or (prediff <=0 and curdiff>0):
                # 注意prediff仅记录摆动时第一次变化的幅度
                res+=1
                prediff = curdiff
        return res
```

## 53. Maximum Subarray

[link](https://leetcode.com/problems/maximum-subarray/description/)

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # 连续和为负数时，抛弃该和，重新计数
        res = -float("inf") # 保留连续和当前最大值，局部最优
        count = 0 # 求连续数字和
        for i in range(len(nums)):
            count+=nums[i]
            # 更新局部最优
            if count>res: res=count
            if count<0: count=0
        return res

```
