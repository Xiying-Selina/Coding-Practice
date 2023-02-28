# Day 27：组合与切割

## 39. Combination Sum

[link](https://leetcode.com/problems/combination-sum/description/)

````python
//```python3
class Solution:
    def __init__(self):
        self.res = []
        self.path = []
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        self.backtracking(candidates, target, 0, 0)
        return self.res

    def backtracking(self, candidates, target, Sum, startindex):
        # 剪枝：当和已经大于target，可以返回
        if Sum>target: return
        # 终止条件：叶子节点Sum==target
        if Sum==target: 
            self.res.append(self.path[:])
            return
        # 单层逻辑
        for i in range(startindex, len(candidates)):
            self.path.append(candidates[i])
            Sum+=candidates[i]
            # 注意可以重复使用元素，递归时用i而不是i+1
            self.backtracking(candidates, target, Sum, i)
            self.path.pop()
            Sum-=candidates[i]

```
````

## 40. Combination Sum II

[link](https://leetcode.com/problems/combination-sum-ii/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res=[]
        self.path=[]

    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        # 注意排序
        sorted_candidates = sorted(candidates)
        used = [False]*len(candidates)
        self.backtracking(sorted_candidates, target,0,0,used)
        return self.res

    def backtracking(self, candidates, target, Sum, startindex,used):
        if Sum>target: return
        if Sum==target:
            self.res.append(self.path[:])
            return
        for i in range(startindex, len(candidates)):
            # 有重复元素，注意去重，树层去重而不是树枝去重
            if i>0 and candidates[i-1]==candidates[i] and used[i-1]==False:
                continue
            self.path.append(candidates[i])
            Sum+=candidates[i]
            used[i]=True
            self.backtracking(candidates, target, Sum, i+1, used)
            self.path.pop()
            Sum-=candidates[i]
            used[i]=False


```
````

## 131. Palindrome Partitioning

[link](https://leetcode.com/problems/palindrome-partitioning/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res=[]
        self.path=[]

    def partition(self, s: str) -> List[List[str]]:
        self.backtracking(s,0)
        return self.res

    def isPalindrome(self, s: str) -> bool:
        return True if s==s[::-1] else False
    
    def backtracking(self, s, startindex):
        # startindex起到切割符的作用
        # Base Case
        if startindex >= len(s): 
            self.res.append(self.path[:])
            return
        # 单层逻辑
        for i in range(startindex, len(s)):
            # 判断切割子串是否为palindrome
            if self.isPalindrome(s[startindex:i+1]):
                self.path.append(s[startindex:i+1])
                self.backtracking(s,i+1)
                self.path.pop()


```
````
