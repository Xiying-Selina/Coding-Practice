# Day 36

## 435. Non-overlapping Intervals

[link](https://leetcode.com/problems/non-overlapping-intervals/description/)

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        count=0
        # 按照左边界排序
        intervals.sort(key=lambda x:(x[0],x[1]))
        # intervals = [[1,2],[1,3],[2,3],[3,4]]
        right = intervals[0][1]
        for i in range(1, len(intervals)):
            # 没有重叠时，右边界更新
            if intervals[i][0]>=right:
                right = intervals[i][1]
            # 有重叠时，右边界更新为两个右边界中最小值
            else:
                right = min(right, intervals[i][1])
                count+=1
        return count
```

## 763. Partition Labels

[link](https://leetcode.com/problems/partition-labels/description/)

```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        res = []
        # 首先遍历s，得到每个字符最后出现的位置，存入map
        hash = [0]*26
        for i in range(len(s)):
            hash[ord(s[i])-ord('a')]=i
        # 将出现过的最大index作为右边界，当该右边界与map存的数值相等时，切割字符串
        left, right = 0, 0 # 分别记录左右边界
        for i in range(len(s)):
            right = max(right, hash[ord(s[i])-ord('a')])
            if i == right:
                res.append(right-left+1)
                left = i+1
        return res
```

## 56. Merge Intervals

[link](https://leetcode.com/problems/merge-intervals/description/)

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if len(intervals)==0: return intervals
        # 先按照左边界进行排序
        intervals.sort(key=lambda x: (x[0],x[1]))
        res = [intervals[0]] #要初始化，否则遍历从第二个开始
        for i in range(1, len(intervals)):
            last = res[-1] # 上一个区间
            # 如果与上一个区间有重叠，此时左边界左<=右，右边界更新为更大的
            if intervals[i][0]<=last[1]:
                res[-1] = [last[0], max(last[1], intervals[i][1])]
            # 与上一个区间无重叠，右边界更新为当前的
            else:
                res.append(intervals[i])
        return res
```
