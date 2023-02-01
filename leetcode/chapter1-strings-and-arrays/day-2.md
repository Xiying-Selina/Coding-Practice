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

```
// Some code
```
