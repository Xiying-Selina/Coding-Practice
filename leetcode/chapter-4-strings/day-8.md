# Day 8

## 28. Find the Index of the First Occurrence in a String

[Link](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

````python
// ```python3
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        # haystack遍历
        #约等于滑动窗口，把指向needle的指针向后移动，不匹配则将指向haystack的指针后移
        for i in range(len(haystack)- len(needle)+1):
            #对于每一个i
            for j in range(len(needle)):
                if needle[j]!=haystack[i+j]:
                    break
                if j ==len(needle)-1:
                    return i
        return -1

```
````

## 459. Repeated Substring Pattern

[Link](https://leetcode.com/problems/repeated-substring-pattern/description/)

````python
// ```python3
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        sub = str()
        for i in range(len(s)//2):
            sub+=s[i]
            if sub*(len(s)//(i+1))==s:
                return True
        return False

```
````
