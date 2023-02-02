# Day 2:

## 977. Squares of a Sorted Array

1. Since the array is non-descending, it's easy to come up with two pointers. The squared numbers in each sides would be greater than the squared numbers in the middle.
2. Use two pointers to point the begin and the end, compare the suqared numbers of at each point. Move the pointers to the middle until they iterate all numbers in the list.

````
// ```python3
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        begin, end = 0, len(nums)-1
        k = len(nums)-1
        res = [None]*(len(nums))
        while(begin<=end):
            if nums[begin]**2>nums[end]**2:
                res[k] = nums[begin]**2
                begin+=1
            else:
                res[k] = nums[end]**2
                end-=1
            k-=1
        return res
```
````

## 209. Minimum Size Subarray Sum

````
// ```python3
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        begin, end = 0, 0
        sums = 0
        res = len(nums)+1
        for end in range(len(nums)):
            sums += nums[end]
            while(sums >= target):
                res = min(res, end-begin+1)
                sums -= nums[begin]
                begin +=1
        # Don't forget to test edge case
        if res == len(nums)+1:
            res = 0
        return res
```
````

## 59. Spiral Matrix II

````
// ```python3
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        # record the starting point of each loop
        xrow, ycol = 0, 0
        num=1
        nums = [[0]* n for _ in range(n)]
        loop = n//2
        offset = 1

        for offset in range(1, loop+1):
            # loop of a square
            # left to right
            for i in range(ycol, n-offset):
                nums[xrow][i] = num
                num+=1
            # top to bottom
            for j in range(xrow,n-offset):
                nums[j][n-offset] = num
                num+=1
            # right to left
            for i in range(n-offset, ycol,-1):
                nums[n-offset][i] = num
                num+=1
            # bottom to top
            for j in range(n-offset, xrow, -1):
                nums[j][ycol]= num
                num+=1
            # change xrow and ycol for next staring point
            xrow+=1
            ycol+=1
        
        # notice if n is odd, there will be a mid point
        if n % 2!=0:
            mid = n//2
            nums[mid][mid] = num
        return nums

        
```
````
