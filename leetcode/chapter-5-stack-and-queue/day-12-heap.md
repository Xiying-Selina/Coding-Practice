# Day 12: Heap

## 347. Top K Frequent Elements

[Link](https://leetcode.com/problems/top-k-frequent-elements/description/)

````python
// ```python3
#时间复杂度：O(nlogk)
#空间复杂度：O(n)
import heapq # min heap
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 1. map统计所有元素出现次数
        res = {} # {元素：出现次数}
        for i in range(len(nums)):
            res[nums[i]] = res.get(nums[i], 0)+1
        # 2. 对频率排序，采用heap，min heap（每次pop最小值）
        # 定义一个min heap，大小为k
        que = []
        # 用heap遍历所有频率
        for key, freq in res.items():
            heapq.heappush(que, (freq, key)) # 按照freq排序所以先freq再key
            if len(que)> k: # 如果堆的长度大于k，则弹出，维护堆的长度
                heapq.heappop(que)
        # 找出前k个高频元素，应该倒序输出数组
        ans= [0]*k
        for i in range(k-1, -1, -1):# [0, k-1]
            ans[i] = heapq.heappop(que)[1] #输出的是key的值，所以是[1]
        return ans

```
````

## 239. Sliding Window Maximum

[Link](https://leetcode.com/problems/sliding-window-maximum/description/)

````python
// ```python3
from collections import deque
# 维护一个单调队列，将有可能的最大值放于队口
# 定义三个函数，pop，push，getMaxValue
class MyQueue:
    def __init__(self):
        self.queue = deque()
    # 每次pop之前确定要弹出的数值是否等于队口的数值，如果是就弹出
    def pop(self, val):
        if self.queue and val==self.queue[0]:
            self.queue.popleft()
    # 每次push的数值都要确定比队口的数值小才push进去，否则就将队列后端的数弹出，直到比队口小
    def push(self, val):
        while self.queue and val>self.queue[-1]:
            self.queue.pop()
        self.queue.append(val)
    # 查询当前队列的最大值，即队口元素
    def getMaxValue(self):
        return self.queue[0]

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        #遍历nums，用que维护遍历过的元素，res记录最大值
        que = MyQueue()
        res=[]
        #初始化que和res，用前k个元素
        for i in range(k):
            que.push(nums[i])
        res.append(que.getMaxValue())
        #遍历nums，更新res，滑动窗口长度为k
        for i in range(k, len(nums)):
            #移除前面的元素
            que.pop(nums[i-k])
            #插入后面的元素
            que.push(nums[i])
            #记录队口最大的元素
            res.append(que.getMaxValue())
        return res



```
````
