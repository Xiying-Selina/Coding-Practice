# Day 15: 层序遍历+翻转+对称

## 102. Binary Tree Level Order Traversal

[Link](https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/898028318/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque 
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        # 借助队列保存已经遍历的元素
        res = [] #保存结果
        if root is None:
            return res
        que = deque([root]) #从根节点开始
        while que:
            size = len(que) # size记录本层的node数量
            temp = [] # temp记录每层的节点
            for i in range(size):#遍历当层，pop当层节点，push子节点，size--
                cur = que.popleft()
                temp.append(cur.val)
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            res.append(temp) #所有层结果
        return res
```
````

##
