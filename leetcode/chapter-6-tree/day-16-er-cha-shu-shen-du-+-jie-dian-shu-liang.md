# Day 16: 二叉树深度+节点数量

## 104. Maximum Depth of Binary Tree

Link

可以用层序遍历或者后序遍历

### 层序遍历（见day15）

````
// // ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        # 使用层序遍历比较合适，因为最大的深度即层数
        if root is None:
            return 0
        que=deque([root])
        depth = 0 #记录层数
        while que:
            size = len(que)
            for i in range(size):
                cur = que.popleft()
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            depth+=1
        return depth

```
````

### 后序遍历

```python
// Some code
```

## 559. Maximum Depth of N-ary Tree

Link

```python
// Some cod
```

## 111. Minimum Depth of Binary Tree

Link

### 层序遍历（见day15）

````python
// // ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        # 与104最大深度相似，只是当左右孩子都为空的时候，才说明是遍历的最低点
        if root is None:
            return 0
        que=deque([root])
        depth=0
        while que:
            size=len(que)
            depth+=1
            for i in range(size):
                cur=que.popleft()
                if cur.left is None and cur.right is None:
                    return depth
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
        return 0

```
````

### 后序遍历

```python
// Some code
```

## 222. Count Complete Tree Nodes

Link

```python
// Some code
```
