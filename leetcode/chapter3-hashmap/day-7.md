# Day 7

## 454. 4Sum II

[Link](https://leetcode.com/problems/4sum-ii/description/)

````python
//```python3
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        res={} #存放前两个list数字和的可能情况，数字和：个数
        count=0
        # 4个list看成两组
        # 先遍历前两组
        for i in nums1:
            for j in nums2:
                if i+j not in res.keys():
                    res[i+j] = 1
                else:
                    res[i+j] +=1
        # 看后两组
        for i in nums3:
            for j in nums4:
                if 0-(i+j) in res.keys():
                    count+=res[0-(i+j)]
        return count


```
````

## 383. Ransom Note

[Link](https://leetcode.com/problems/ransom-note/description/)

````python
// ```python3
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        res=[0]*26
        # 记录magzine里面字母出现的次数
        for i in magazine:
            res[ord(i)-ord('a')]+=1
        for i in ransomNote:
            if res[ord(i)-ord('a')]<=0:
                return False
            else:
                res[ord(i)-ord('a')]-=1
        return True
```
````

## 13. 3Sum

[Link](https://leetcode.com/problems/3sum/description/)

````python
//```python3
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # 不可以包含重复triplets，hashmap去重容易超时，此题可以用双指针
        # 因为返回值是数值而非index，排序+双指针可行
        nums = sorted(nums)
        ans = []
        for i in range(len(nums)):
            # 已经排序情况下，如果首元素就大于0， 那么没有解
            if nums[i]>0:
                return ans
            # 注意如果有连续几个相同的数值，应该越过相同的数值
            # [-4,-1,-1,0,1,2] i=1: -1, left:0, right:1; i=2:-1, left:0, right:1重复
            if i>0 and nums[i]==nums[i-1]:
                continue
            # 每一个元素之后的区间内，用双指针进行查找
            left, right = i+1, len(nums)-1
            while left<right:
                # 移动左右指针
                if nums[i]+nums[left]+nums[right]>0:
                    right-=1
                elif nums[i]+nums[left]+nums[right]<0:
                    left+=1
                else:
                    ans.append([nums[i], nums[left], nums[right]])
                    # 比如[-1,-1,-1,1,2]， i=0, left=1, right=4,之后left=2会生成同样的解
                    while left != right and nums[left]==nums[left+1]: left+=1
                    while left != right and nums[right]==nums[right-1]: right-=1
                    # 找到满足的解后，两端指针都移动
                    left+=1
                    right-=1
        return ans
                


```
````

## 18. 4Sum

[Link](https://leetcode.com/problems/4sum/)

````python
// ```python3
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        # 类似三数之和，可以想到双指针的方法
        nums= sorted(nums)
        ans=[]
        for i in range(len(nums)):
            if i>0 and nums[i]==nums[i-1]: continue
            for j in range(i+1, len(nums)):
                if j>i+1 and nums[j]==nums[j-1]: continue
                left, right = j+1, len(nums)-1
                while left<right:
                    if nums[i]+nums[j]+nums[left]+nums[right]>target:
                        right-=1
                    elif nums[i]+nums[j]+nums[left]+nums[right]<target:
                        left+=1
                    else:
                        ans.append([nums[i],nums[j],nums[left],nums[right]])
                        while left!=right and nums[left]==nums[left+1]: left+=1
                        while left!=right and nums[right]==nums[right-1]: right-=1
                        right-=1
                        left+=1
        return ans


```
````
