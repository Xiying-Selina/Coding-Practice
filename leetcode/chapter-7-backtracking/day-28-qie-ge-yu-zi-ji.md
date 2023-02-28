# Day 28：切割与子集

## 93. Restore IP Addresses

[link](https://leetcode.com/problems/restore-ip-addresses/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res:List[str] = []

    def restoreIpAddresses(self, s: str) -> List[str]:
        if len(s)>12:return []
        self.backtracking(s,0,0)
        return self.res

    def isValid(self,s,begin,end):
        if begin>end: return False
        # 以0开头不合法
        if s[begin]=='0' and begin<end: return False
        # 大于255不合法
        if int(s[begin:end+1])>255: return False
        return True

    def backtracking(self, s, startindex, pointSum):
        # pointSum记录每一个分割内的数字个数
        # startindex作分割符
        # Base Case: 到三位数时则终止
        if pointSum==3:
            # 需要对最后一段s[startindex,len(s)-1]进行合法判断，并且记录结果
            if self.isValid(s,startindex,len(s)-1):
                self.res.append(s[:])
                return
        for i in range(startindex,len(s)):
            if self.isValid(s, startindex, i):
                # 在切割点i+1处插入"."
                s = s[:i+1]+"."+s[i+1:]
                pointSum+=1
                # 因为加入了"."，下一位数字后移为i+2
                self.backtracking(s,i+2,pointSum)
                s = s[:i+1]+s[i+2:]
                pointSum-=1
            else:
                break
```
````

## 78. Subsets

[link](https://leetcode.com/problems/subsets/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res=[]
        self.path=[]

    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.backtracking(nums,0)
        return self.res

    def backtracking(self,nums,startindex):
        # 收集所有节点，所以在每一层递归都放入
        self.res.append(self.path[:])
        #Base Case
        if startindex>=len(nums): return
        # Recursion and backtracking
        for i in range(startindex, len(nums)):
            self.path.append(nums[i])
            self.backtracking(nums,i+1)
            self.path.pop()
        
```
````

## 90. Subsets II

link

````python
// ```python3
class Solution:
    def __init__(self):
        self.path=[]
        self.res=[]

    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        # 注意排序
        sorted_nums = sorted(nums)
        used = [False]*len(nums)
        self.backtracking(sorted_nums,0,used)
        return self.res

    def backtracking(self, nums, startindex,used):
        self.res.append(self.path[:])
        if startindex>len(nums):return
        for i in range(startindex, len(nums)):
            # 树层去重，保留树枝
            if i>0 and nums[i-1]==nums[i] and used[i-1]==False:
                continue
            self.path.append(nums[i])
            used[i]=True
            self.backtracking(nums,i+1,used)
            self.path.pop()
            used[i]=False
```
````
