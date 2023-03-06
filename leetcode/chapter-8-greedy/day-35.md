# Day 35

## 860. Lemonade Change

[link](https://leetcode.com/problems/lemonade-change/)

```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        # 情况一：账单是5，直接收下。
        # 情况二：账单是10，消耗一个5，增加一个10
        # 情况三：账单是20，优先消耗一个10和一个5，如果不够，再消耗三个5
        five, ten =0, 0
        for bill in bills:
            if bill==5: 
                five+=1
            elif bill==10:
                five-=1
                ten+=1
            else:
                if ten>0 and five>0:
                    ten-=1
                    five-=1
                elif five>=3:
                    five-=3
                else:
                    return False
        return True


```

## 406. Queue Reconstruction by Height

[link](https://leetcode.com/problems/queue-reconstruction-by-height/description/)

```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        # 局部最优：优先按身高高的people的k来插入。插入操作过后的people满足队列属性
        # 全局最优：最后都做完插入操作，整个队列满足题目队列属性
        # 先按照身高(维度h）从大到小排序，再按照（维度k）从小到大排序
        people.sort(key=lambda x:(-x[0],x[1]))
        res=[]
        # 根据每个元素的第二个维度k，贪心算法，进行插入
        # people已经排序过了：同一高度时k值小的排前面
        # people = [[7,0], [7,1], [6,1], [5,0], [5,2], [4,4]]
        for person in people:
            # 在person[1]位置前面插入person
            res.insert(person[1],person)
        return res
```

## 452. Minimum Number of Arrows to Burst Balloons&#x20;

[link](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)

````python
//```python3
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        # 局部最优：当气球出现重叠，一起射，所用弓箭最少。
        # 全局最优：把所有气球射爆所用弓箭最少。
        # 让气球尽可能的重叠，需要对数组进行排序
        # 如果气球重叠了，重叠气球中右边边界的最小值之前的区间一定需要一个弓箭。
        if len(points)==0: return 0
        points.sort(key=lambda x:x[0])
        # points = [[1,6],[2,8],[7,12],[10,16]]
        res=1
        for i in range(1, len(points)):
            if points[i][0]>points[i-1][1]: # 气球两边不挨着
                res+=1
            else:
                # points = [[1,6],[2,6],[7,12],[10,12]], res=2
                points[i][1]=min(points[i][1], points[i-1][1])# 更新重叠气球最小右边界
        return res
```
````
