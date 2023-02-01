# Day 1: Binary Search & Two Pointers

## 704. Binary Search

Binary Search is a searching algorithm used in a sorted array by repeatedly dividing the search interval in half. The idea of binary search is to use the information that the array is sorted and reduce the time complexity to O(Log n).

```
// class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)-1
        while(left <=right):
            middle = left+(right-left)//2
            if nums[middle]<target:
                left = middle+1
            elif nums[middle]>target:
                right = middle-1
            else:
                return middle
        return -1
```

## 27. Remove Element

Usage of two pointers.

```
// class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow, fast = 0,0

        while fast < len(nums):
            if nums[fast]!=val:
                nums[slow] = nums[fast]
                slow+=1
            fast+=1
        return slow
```

## 26. Remove Duplicates from Sorted Array

```
// class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:

        slow= 0
        for fast in range(1, len(nums)):
            if nums[slow]!=nums[fast]:
                nums[slow+1] = nums[fast]
                slow+=1
        return slow+1  
```

## 28. Move Zeros

```
// class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow = 0
        for fast in range(len(nums)):
            if nums[fast]!=0:
                nums[slow], nums[fast] = nums[fast], nums[slow]
                slow+=1
        return nums
```

## 34. Find First and Last Position of Element in Sorted Array

```
// class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        def lower_num(nums,target):
            left , right = 0, len(nums)-1
            while left<=right:
                middle = left+(right-left)//2
                if nums[middle]>=target:
                    right = middle-1
                else:
                    left = middle+1
            return left

        def upper_num(nums,target):
            left , right = 0, len(nums)-1
            while left<=right:
                middle = left+(right-left)//2
                if nums[middle]<=target:
                    left = middle+1
                else:
                    right = middle-1
            return right

        low = lower_num(nums,target)
        upp = upper_num(nums,target)
        if low<=upp:
            return [low,upp]
        return [-1,-1]
```

## 35. Search Insert Position

```
// class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)-1
        while left<=right:
            middle = left+(right-left)//2
            if nums[middle]>target:
                right = middle-1
            elif nums[middle]<target:
                left = middle +1
            else:
                return middle
        return right+1
```
