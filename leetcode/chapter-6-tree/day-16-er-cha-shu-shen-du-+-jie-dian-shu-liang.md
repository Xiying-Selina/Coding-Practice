# Day 16: 二叉树深度+节点数量

## 104. Maximum Depth of Binary Tree

[Link](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

可以用层序遍历或者后序遍历

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

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        # postorder: left,right,parent
        return self.getdepth(root)


    def getdepth(self, node):
        # 1. parameter and return value
        # 2. end circumstances
        if not node:
            return 0
        # postorder: left,right,parent
        ldepth = self.getdepth(node.left)
        rdepth = self.getdepth(node.right)
        depth = 1+max(ldepth, rdepth) #左右子树最大的高度+本层
        return depth

```
````

## 559. Maximum Depth of N-ary Tree

[Link](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/description/)

### 层序遍历

````python
// ```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
from collections import deque
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        # 层序遍历： 找到层数，即最大深度
        depth = 0
        if not root:
            return 0
        que = deque([root])
        while que:
            size=len(que)
            depth+=1
            for i in range(size):
                cur=que.popleft()
                if cur.children:
                    # children>=2时，将所有子节点加入需要用extend
                    que.extend(cur.children)
        return depth

```
````

### 后序遍历

````python
// ```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def maxDepth(self, root: 'Node') -> int:
        # postorder : left, right, parent
        # N: children, parent
        return self.getdepth(root)

    def getdepth(self,node):
        if not node:
            return 0
        depth = 0
        # 后序遍历的所有孩子，获得每一条枝干的长度，更新最大深度
        for i in range(len(node.children)):
            child_depth = self.getdepth(node.children[i])
            depth = max(depth, child_depth)
        # 等价于后序遍历的“中”，加上本层
        depth+=1
        return depth
        
```
````

## 111. Minimum Depth of Binary Tree

[Link](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

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

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        # postorder: left, right, parent
        return self.getdepth(root)

    def getdepth(self, node):
        if not node:
            return 0
        ldepth = self.getdepth(node.left)
        rdepth = self.getdepth(node.right)
        # 若只用1+min(ldepth, rdepth)，会出现根节点没有叶子节点的情况
        # 只有当左右孩子都为空的时候，才说明遍历到最低点
        if not node.left and node.right:
            return 1+rdepth
        if node.left and not node.right:
            return 1+ldepth
        depth = 1+min(ldepth, rdepth)
        return depth

```
````

## 222. Count Complete Tree Nodes

[Link](https://leetcode.com/problems/count-complete-tree-nodes/description/)

### 层序遍历

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
    def countNodes(self, root: Optional[TreeNode]) -> int:
        # 普通二叉树也可以的方法
        # 层序遍历，遍历每层的节点数量
        if not root:
            return 0
        res=0
        que=deque([root])
        while que:
            size=len(que)
            for i in range(size):
                cur=que.popleft()
                res+=1
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
        return res

```
````

### 后序遍历

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        # 后序遍历：普通二叉树也可以使用的方法
        # postorder: left, right, parent
        return self.getNum(root)

    def getNum(self, node):
        if not node:
            return 0
        lcount = self.getNum(node.left) # left
        rcount = self.getNum(node.right) # right
        count = lcount+rcount+1 #左子树个数+右子树个数+自己
        return count
        
        
```
````

### 完全二叉树

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        # 完全二叉树只有两种情况，情况一：就是满二叉树，情况二：最后一层叶子节点没有满。
        # 对于情况一，可以直接用 2^树深度 - 1 来计算，注意这里根节点深度为1。
        # 对于情况二，分别递归左孩子，和右孩子，递归到某一深度一定会有左孩子或者右孩子为满二叉树，然后依然可以按照情况1来计算。
        if not root:
            return 0
        # 在完全二叉树中，如果递归向左遍历的深度等于递归向右遍历的深度，那说明就是满二叉树。
        # 求左子树深度
        left = root.left
        right = root.right
        leftDepth = 0 #这里初始为0是有目的的，为了下面求指数方便
        rightDepth = 0
        while left: #求左子树深度
            left = left.left
            leftDepth += 1
        while right: #求右子树深度
            right = right.right
            rightDepth += 1
        if leftDepth == rightDepth:
            return (2 << leftDepth) - 1 #注意(2<<1) 相当于2^2，所以leftDepth初始为0
        return self.countNodes(root.left) + self.countNodes(root.right) + 1
```
````
