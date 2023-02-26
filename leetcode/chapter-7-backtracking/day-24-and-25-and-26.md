# Day 24 & 25 & 26

## 77. Combinations

[link](https://leetcode.com/problems/combinations/description/)

````python
// ```python3
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        # 保存结果
        res=[]
        path=[]
        # 回溯
        def backtracking(n, k, startindex):
            # if(终止条件):收集结果；return
            if len(path)==k:
                res.append(path[:])
                return
            # for(集合元素集)：处理结果；递归；回溯
            # 剪枝， 最后k - len(path)个节点直接构造结果，无需递归
            last_startindex = n-(k-len(path))+1
            for i in range(startindex, last_startindex+1):
                path.append(i)
                backtracking(n, k, i+1)
                path.pop()
        backtracking(n,k,1)
        return res
```
````

## 216. Combination Sum III

[link](https://leetcode.com/problems/combination-sum-iii/description/)

````python
// ```python3
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res=[]
        path=[]
        def backtracking(n,k,sums,startindex):
            # 剪枝1：如果sums已经超过n，不用继续遍历
            if sums>n: return
            if(len(path)==k):
                if sums==n: res.append(path[:])
                return
            # 剪枝2：最后k-len(path)个结果可以直接构造，不用递归
            for i in range(startindex, 10-(k-len(path))+1):
                sums+=i
                path.append(i)
                backtracking(n,k,sums,i+1)
                sums-=i
                path.pop()
        backtracking(n,k,0,1)
        return res
```
````

## 17. Letter Combinations of a Phone Number

[link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res_lst:List[str]=[] #保存结果
        self.res_str:str='' #s记录可能的字母组合
        self.letter_map={
            '2':'abc',
            '3':'def',
            '4':'ghi',
            '5':'jkl',
            '6':'mno',
            '7':'pqrs',
            '8':'tuv',
            '9':'wxyz'
        }
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits: return []
        self.backtracking(digits,0)
        return self.res_lst

    def backtracking(self, digits,index): 
            #index记录当前遍历的数字的位置
            if len(digits)==index:
                self.res_lst.append(self.res_str)
                return
            # letter表示此时digit的数字对应的字母组合
            letters:str=self.letter_map[digits[index]]
            for letter in letters:
                self.res_str += letter
                self.backtracking(digits, index+1)
                self.res_str=self.res_str[:-1] #popback
                



```
````
