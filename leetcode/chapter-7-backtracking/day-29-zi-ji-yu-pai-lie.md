# Day 29: 子集与排列

## 491. Non-decreasing Subsequences

[link](https://leetcode.com/problems/non-decreasing-subsequences/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res=[]
        self.path=[]

    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        # 本题中需要注意，不能排序后用used记录，否则改变子集的顺序
        self.backtracking(nums,0)
        return self.res

    def backtracking(self,nums,startindex):
        # 子集问题，收集所有符合条件的节点，本题中需要path>1
        if len(self.path)>1: self.res.append(self.path[:])
        # 定义一个set，记录取过的数
        uset = set()
        # 同层横向遍历
        for i in range(startindex, len(nums)):
            # 若当前元素值非递增，或者曾用过，跳入下一循环
            if (self.path and nums[i]<self.path[-1] )or nums[i] in uset:
                continue
            uset.add(nums[i])
            self.path.append(nums[i])
            self.backtracking(nums, i+1)
            # uset不需要回溯，因为只记录本层，在每一个递归中会重新定义
            self.path.pop()
```
````

## 46. Permutations

[link](https://leetcode.com/problems/permutations/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.path=[]
        self.res=[]

    def permute(self, nums: List[int]) -> List[List[int]]:
        used=[False]*len(nums)
        self.backtracking(nums,used)
        return self.res

    def backtracking(self, nums,used):
        # permutation不需要startindex，因为顺序有必要
        if len(self.path)==len(nums):
            self.res.append(self.path[:])
            return
        for i in range(0, len(nums)):
            # 树枝去重
            if used[i]==True: continue
            self.path.append(nums[i])
            used[i]=True
            self.backtracking(nums, used)
            self.path.pop()
            used[i]=False
```
````

## 47. Permutations II

[link](https://leetcode.com/problems/permutations-ii/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res=[]
        self.path=[]

    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        sorted_nums = sorted(nums)
        used=[False]*len(nums)
        self.backtracking(sorted_nums, used)
        return self.res

    def backtracking(self, nums, used):
        if len(self.path)==len(nums): 
            self.res.append(self.path[:])
            return
        for i in range(0,len(nums)):
            # 树层去重
            if i>0 and nums[i-1]==nums[i] and used[i-1]==False: continue
            if used[i]==True: continue
            self.path.append(nums[i])
            used[i]=True
            self.backtracking(nums,used)
            self.path.pop()
            used[i]=False
```
````
