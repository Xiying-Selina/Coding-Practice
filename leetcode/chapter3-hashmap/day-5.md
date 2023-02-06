# Day 5

## 242. Valid Anagram

[Link](https://leetcode.com/problems/valid-anagram/description/)

````python
// ```python3
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # 用records作为空表，记录26个字母
        records = [0]*26
        # 分别遍历两个字符串，第一个字符给每个出现过的加一，第二个减一
        for i in s:
            records[ord(i)-ord('a')]+=1
        for j in t:
            records[ord(j)-ord('a')]-=1
        # 如果表中有不为0的，说明不是anagram
        for k in range(len(records)):
            if records[k] != 0:
                return False
        return True
```
````

## 349. Intersection of Two Arrays

[Link](https://leetcode.com/problems/intersection-of-two-arrays/description/)

````python
// ```python3
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        records = set()
        res = []
        for num in nums1:
            records.add(num)
        for num in nums2:
            if num in records:
                res.append(num)
                records.remove(num)
        return res
```
````

## 202. Happy Number

[Link](https://leetcode.com/problems/happy-number/description/)

````python
// ```python3
class Solution:
    def isHappy(self, n: int) -> bool:
        # 记录出现过的每一个数字，如果成为循环，必然有重复的数字
        records = set()
        while n!= 1:
            # 求新的数字
            new_num=0
            for i in str(n):
                new_num += int(i)**2
            # 出现循环就停止
            if new_num in records:
                return False
            # 没有循环则记录新的n
            n=new_num
            records.add(n)
        return True
```
````

## 1. Two Sum

[Link](https://leetcode.com/problems/two-sum/description/)

````python
// ```python3
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 用records记录出现过的数字，以及他们的index
        # 需要记录value和index，则需要用dict来记录
        records = {}
        ans = []
        for i in range(len(nums)):
            if target-nums[i] not in records.keys():
                records[nums[i]] = i #记录出现过的数字及位置
            else:
                ans.append(records[target-nums[i]])
                ans.append(i)
        # 返回值是index
        return ans
```
````

## 1002. Find Common Characters

[Link](https://leetcode.com/problems/find-common-characters/)

````python
// ```python3
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        # 用第一个单词初始化
        ans=[]
        records=[0]*26
        for letter in words[0]:
            records[ord(letter)-ord('a')]+=1
        for i in range(1, len(words)):
            temp=[0]*26
            for letter in words[i]:
                temp[ord(letter)-ord('a')]+=1
            for letter in range(26):
                records[letter] = min(temp[letter], records[letter])
        # 遍历records
        for i in range(26):
            while records[i]!=0:
                ans.append(chr(i+ord('a')))
                records[i] -=1
        return ans
```
````
