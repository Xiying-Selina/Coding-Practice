# Day 7

## 344. Reverse String

[Link](https://leetcode.com/problems/reverse-string/description/)

````python
// ```python3
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s)-1
        while left<right:
            s[left], s[right] = s[right], s[left]
            left+=1
            right-=1
        return s
```
````

## 541. Reverse String II

[Link](https://leetcode.com/problems/reverse-string-ii/)

````python
// ```python3
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # 用list存放结果
        res=[i for i in s]
        # 定义reverse的函数，和库函数reverse一致
        def reverseSub(res):
            left,right=0, len(res)-1
            while left<right:
                res[left], res[right] = res[right], res[left]
                left+=1
                right-=1
            return res
        # 在每一个s中每步2k遍历，对每一个2k，将前面的k个翻转
        for i in range(0,len(res), k*2):
            res[i:i+k]=reverseSub(res[i:i+k])
        return "".join(res)

```
````

## 剑指 Offer 05. 替换空格

[Link](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

````python
// ```python3
class Solution:
    def replaceSpace(self, s: str) -> str:
        res=[i for i in s.split(" ")]
        return "%20".join(res)
```
````

## 151. Reverse Words in a String

[Link](https://leetcode.com/problems/reverse-words-in-a-string/description/)

````python
// ```python3
class Solution:
    def reverseWords(self, s: str) -> str:
        res = reversed(s.split())
        return " ".join(res)
```
````

````python
// ```python3
class Solution:
#    def reverseWords(self, s: str) -> str:
#        res = reversed(s.split())
#        return " ".join(res)

    #  If the string data type is mutable in your language, can you solve it in-place with O(1) extra space?
    # 不使用库函数，在字符串直接进行
    # 1. 移除多余空格：这一步需要遍历完整的字符串
    def remove_space(self, s:str) -> list:
        left, right =0, len(s)-1
        # 移除首位的空格，中间的空格只保留一个
        while left<=right and s[left]==" ":
            left+=1
        while left<=right and s[right]==" ":
            right-=1
        res=[]
        while left<=right:
            if s[left]!=" ":
                res.append(s[left])
            # 如果一个空格没有被放进去，要left再移动一次，放进去一个空格
            elif res[-1]!=" ":
                res.append(s[left])
            left+=1
        return res

        # 2. 反转字符串
    def reverse_string(self,lst:list,left:int, right:int):
        while left<right:
            lst[left], lst[right] = lst[right], lst[left]
            left+=1
            right-=1

        # 3. 反转每个单词
    def reverse_word(self,lst:list):
        begin, end = 0, 0 #找每个单词的起点和终点
        for end in range(len(lst)):
            # end到单词末尾开始反转，此时end指向空格或者最末尾字母
            if lst[end]==" " and end!=len(lst)-1:
                self.reverse_string(lst, begin, end-1)
                begin=end+1
                end+=1
            elif end==len(lst)-1:
                self.reverse_string(lst, begin, end)

    def reverseWords(self, s: str) -> str:
        res = self.remove_space(s)
        self.reverse_string(res, 0, len(res)-1)
        self.reverse_word(res)
        return "".join(res)


```
````

## 剑指 Offer 58 - II. 左旋转字符串

[Link](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

````python
// ```python3
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        lst = list(s)
        # 1. 反转区间为前[0:n-1]的子串
        lst[0:n] = reversed(lst[0:n])
        # 2. 反转区间为[n:]到末尾的子串
        lst[n:] = reversed(s[n:])
        # 3. 反转整个字符串
        lst = reversed(lst)
        return "".join(lst)

```
````
