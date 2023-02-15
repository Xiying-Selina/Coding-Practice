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

## 107. Binary Tree Level Order Traversal II

[Link](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/)

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
    def levelOrderBottom(self, root: Optional[TreeNode]) -> List[List[int]]:
        # 用一个queue实现层序遍历
        res = [] #保存结果
        if root is None:
            return res
        que = deque([root]) # 初始化que
        while que:
            size = len(que) #每一层的节点个数
            temp = [] #每一层节点
            for i in range(size):#pop该节点，push子节点
                cur = que.popleft()
                temp.append(cur.val)
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            res.append(temp)

        res.reverse()
        return res

```
````

## 199. Binary Tree Right Side View

[Link](https://leetcode.com/problems/binary-tree-right-side-view/submissions/898127896/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        if root is None:
            return res
        que = deque([root])
        while que:
            size= len(que)
            temp = []#与层序遍历的区别是，每次存下来的是当层的最后一个数
            for i in range(size):
                cur = que.popleft()
                temp.append(cur.val)
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            res.append(temp[-1])
        return res
            
```

## 637. Average of Levels in Binary Tree

[Link](https://leetcode.com/problems/average-of-levels-in-binary-tree/submissions/898136370/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:
        res = []
        if root is None:
            return res
        que = deque([root])
        while que:
            size = len(que)
            sums = 0
            for i in range(size):
                cur = que.popleft()
                sums += cur.val
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            res.append(sums/size)
        return res

```

## 429. N-ary Tree Level Order Traversal

[Link](https://leetcode.com/problems/n-ary-tree-level-order-traversal/submissions/898140278/)

```python
// """
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
from collections import deque
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        # 层序遍历，只是每一个node可以有多个child
        res=[]
        if root is None:
            return res
        que = deque([root])
        while que:
            size = len(que)
            temp=[]
            for i in range(size):
                cur = que.popleft()
                temp.append(cur.val)
                if cur.children:
                    que.extend(cur.children)
                    # extend与append区别：extend遍历要加进去的list，一个个加入元素
            res.append(temp)
        return res
                
```

## 515. Find Largest Value in Each Tree Row

[Link](https://leetcode.com/problems/find-largest-value-in-each-tree-row/submissions/898143181/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
import math
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        #依然是层序遍历
        res=[]
        if root is None:
            return res
        que = deque([root])
        while que:
            size = len(que)
            max_val = -math.inf
            for i in range(size):
                cur = que.popleft()
                max_val = max(cur.val, max_val)
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            res.append(max_val)
        return res
```

## 116. Populating Next Right Pointers in Each Node

[Link](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)

````python
// ```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
from collections import deque
class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        # 层序遍历
        # 每一层节点指向下一个结点，如果已经是该层最后一个节点，就指向空
        if root is None:
            return None
        que = deque([root])
        while que:
            size=len(que)
            for i in range(size):
                cur = que.popleft()
                # cur记录每一层遍历到的第一个节点
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
                # 如果是最后一个节点，就退出循环
                if i==size-1:
                    break
                cur.next = que[0] #此时指针指向下一个节点
        return root
            
                        

```
````

## 117. Populating Next Right Pointers in Each Node II

[Link](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)

````python
// ```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
from collections import deque
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        #层序遍历写法
        if root is None:
            return None
        que = deque([root])
        while que:
            size = len(que)
            for i in range(size):
                cur = que.popleft()
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
                if i==size-1:
                    break
                cur.next = que[0]
        return root
```
````

## 104. Maximum Depth of Binary Tree

[Link](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

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

## 111. Minimum Depth of Binary Tree

[Link](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

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

## 226. Invert Binary Tree

[Link](https://leetcode.com/problems/invert-binary-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        # 可以用前序遍历或者后序遍历
        if root is None:
            return None
        #后序遍历：左右中
        self.invertTree(root.left) #左
        self.invertTree(root.right) #右
        root.left, root.right = root.right, root.left #中
        return root

```
````

## 101. Symmetric Tree

[Link](https://leetcode.com/problems/symmetric-tree/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        # 后序遍历：适用于需要把下层信息传递至上层的树
        if root is None:
            return True
        return self.compare(root.left, root.right)

    def compare(self, left, right):
        # 排除空节点情况：有一边空，两边都空
        if left is None and right is None: return True
        elif left and right is None: return False
        elif left is None and right: return False
        # 排除数值不同的情况
        elif left.val!=right.val: return False
        # 当前左右节点均不为空，且数值相同
        # 后序：左右中, 即外层，内层，上一层
        outside = self.compare(left.left, right.right) # 左子树左vs右子树右
        inside = self.compare(left.right, right.left) #左子树右vs右子树左
        isSame = outside and inside
        return isSame
```
````

## 100. Same Tree

[Link](https://leetcode.com/problems/same-tree/submissions/898275291/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # 与101.Symmetric Tree相似，可以用后序遍历
        # 因为需要把下层信息传递到上层

        # null check & value unequal check
        if p is None and q is None: return True
        elif p and q is None: return False
        elif p is None and q: return False
        elif p.val !=q.val: return False

        # postorder: left, right,parent
        lSame = self.isSameTree(p.left, q.left)
        rSame = self.isSameTree(p.right, q.right)
        isSame = lSame and rSame
        return isSame
```

## 572. Subtree of Another Tree

[Link](https://leetcode.com/problems/subtree-of-another-tree/submissions/898286791/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        # 与101.Symmetric Tree相似，可以用后序遍历
        # 因为需要把下层信息传递到上层
        if root is None: return False
        elif self.isIdentical(root, subRoot): return True
        return self.isSubtree(root.left,subRoot) or self.isSubtree(root.right,subRoot)

    def isIdentical(self,root, subRoot):
        # null check
        if root is None and subRoot is None: return True
        elif root is None and subRoot: return False
        elif root and subRoot is None: return False
        # postorder: left, right, parent
        lcheck = self.isIdentical(root.left, subRoot.left)
        rcheck = self.isIdentical(root.right, subRoot.right)
        subcheck = root.val==subRoot.val and lcheck and rcheck
        return subcheck
```
