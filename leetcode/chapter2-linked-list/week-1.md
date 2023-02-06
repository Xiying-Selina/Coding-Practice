# Week 1

## 702. Search in a Sorted Array of Unknown Size

[Link](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/description/)

````python
// ```python3
# """
# This is ArrayReader's API interface.
# You should not implement it, or speculate about its implementation
# """
#class ArrayReader:
#    def get(self, index: int) -> int:

class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        # 不知道长度，从头开始遍历寻找的想法是很自然的
        # 用一个区间遍历，然后再在区间内进行二分查找
        # 这个区间的设置: left = 0, right = 1
        # 每一次移动： left = right， right *= 2
        left, right = 0, 1
        while reader.get(right)<target:
            left = right
            right *= 2
        # 此时停在right指向的数值大于等于目标的时候
        # binary search, 移动左右区间
        while left <= right:
            mid = left + (right-left)//2
            if reader.get(mid) == target:
                return mid
            elif reader.get(mid) > target:
                right = mid-1
            else:
                left = mid+1
        return -1

```
````

##

