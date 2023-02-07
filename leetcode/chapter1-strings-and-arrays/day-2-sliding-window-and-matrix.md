# Day 2: Sliding Window & Matrix

## 977. Squares of a Sorted Array

1. Since the array is non-descending, it's easy to come up with two pointers. The squared numbers in each sides would be greater than the squared numbers in the middle.
2. Use two pointers to point the begin and the end, compare the suqared numbers of at each point. Move the pointers to the middle until they iterate all numbers in the list.

````python
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

Sliding Window: begin point and end point

First, move end point to iterate all elements, when the elements in this subarray meet the requirements, move the begin point to narrow down the window.

Update the records of each window, usually the length, which is (end-begin+1). In this case, take the min in each updates.

````python
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



````python
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

## 904. Fruit Into Basket

Run some test cases

````python
// ```python3
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        begin , end = 0, 0
        basket = {}
        sums = 0
        for end in range(len(fruits)):
            basket[fruits[end]] = basket.get(fruits[end], 0)+1
            while len(basket)>2:
                basket[fruits[begin]] -=1
                if basket[fruits[begin]]==0:
                    del basket[fruits[begin]]
                begin+=1                
            sums = max(sums, end-begin+1)
        return sums
```
````

## 54. Spiral Matrix

````python
// ```python3
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result = []
        rows, columns = len(matrix), len(matrix[0])
        up = left = 0
        right = columns - 1
        down = rows - 1

        while len(result) < rows * columns:
            # Traverse from left to right.
            for col in range(left, right + 1):
                result.append(matrix[up][col])

            # Traverse downwards.
            for row in range(up + 1, down + 1):
                result.append(matrix[row][right])

            # Make sure we are now on a different row.
            if up != down:
                # Traverse from right to left.
                for col in range(right - 1, left - 1, -1):
                    result.append(matrix[down][col])

            # Make sure we are now on a different column.
            if left != right:
                # Traverse upwards.
                for row in range(down - 1, up, -1):
                    result.append(matrix[row][left])

            left += 1
            right -= 1
            up += 1
            down -= 1

        return result
```
````
