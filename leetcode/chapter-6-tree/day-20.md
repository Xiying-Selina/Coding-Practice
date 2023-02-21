# Day 20

## 530. Minimum Absolute Difference in BST

link

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        # BST：可中序遍历，同98
        pre=None #储存遍历过的节点
        res=float("inf")
        def __getMinimumDifference(root:TreeNode):
            nonlocal pre
            nonlocal res
            # 停止条件：树为空
            if not root: return 
            __getMinimumDifference(root.left)
            if pre: 
                res=min(res,root.val-pre.val)
            pre=root
            __getMinimumDifference(root.right)
        __getMinimumDifference(root)
        return res


```
````

## 501. Find Mode in Binary Search Tree

[link](https://leetcode.com/problems/find-mode-in-binary-search-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.pre=TreeNode()
        self.count = 0 #记录次数
        self.maxcount=0 #记录mode
        self.res=[] 

    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        self.traversal(root)
        return self.res

    def traversal(self,node):
        if not node: return 
        self.traversal(node.left)
        # 第一个节点
        if not self.pre:
            self.count=1
        # 与前一个node数值相同
        elif node.val==self.pre.val:
            self.count+=1
        # 与前一个数值不同
        else:
            self.count=1
        self.pre=node
        # 判断count和maxcount，更新最大值
        if self.count==self.maxcount:
            self.res.append(node.val)
        elif self.count>self.maxcount:
            self.maxcount=self.count
            # 清空res之前保存的数值，只保留现在的
            self.res=[node.val]
        self.traversal(node.right)
        


        
```
````

## 236. Lowest Common Ancestor of a Binary Tree

[link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        # 后序遍历，因为需要向上传递
        # 终止条件：节点为空，或者已经遍历到需要查找的节点
        if not root or root==p or root==q: return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        # 左右： 如果left 和 right都不为空，说明此时root就是最近公共节点
        if left and right:
            return root 
        # 如果left为空，right不为空，就返回right，说明目标节点是通过right返回的
        if  not left and right:
            return right
        else:
            return left
```
````
