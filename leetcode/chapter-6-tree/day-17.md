# Day 17

## 101. Balanced Binary Tree

[Link](https://leetcode.com/problems/balanced-binary-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        # 明确高度差<=1，采用后序遍历，左右中
        if self.getheight(root)!=-1:
            return True
        else: 
            return False

    # 1. 返回值和参数：返回左右子树高度，传入节点
    def getheight(self, node):
        # 2. 停止条件：节点为空
        if not node:
            return 0
        # 3. 单层情况：左右：返回高度；如果返回的是-1则直接结束
        ldepth = self.getheight(node.left)
        if ldepth==-1: return -1
        rdepth = self.getheight(node.right)
        if rdepth==-1: return -1
        # 中：如果左右高度差大于1，返回-1；否则返回高度即左右最大高度+当层
        if abs(ldepth-rdepth)>1:
            return -1
        else:
            return 1+max(ldepth, rdepth)
```
````

## 257. Binary Tree Paths

[Link](https://leetcode.com/problems/binary-tree-paths/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        # 需要返回所有从上到下遍历的路径，用前序遍历比较合适:中左右
        path=""
        res=[]
        if not root: return res
        self.traversal(root,path,res)
        return res


    def traversal(self, node:TreeNode, path:str, res:list[str]):
        # 1. 确定返回值和参数：需要记录路径和整体的结果
        path+=str(node.val) # 中：先做这一步，不然下一句没有path
        # 2. 确定停止条件：到叶子节点，即没有左右孩子，此时把path加入res
        if not node.left and not node.right:
            res.append(path) # 因为先做了中，不宜用not node，会把None加入path
        # 但接下来需要判断not node，避免空节点
        # 左右：把值加入path，这里的"+>"其实暗含回溯思想
        if node.left: 
            self.traversal(node.left, path+"->", res)
        if node.right:
            self.traversal(node.right, path+"->", res)
        
        
```
````

## 404. Sum of Left Leaves

[Link](https://leetcode.com/problems/sum-of-left-leaves/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        # 后序遍历，因为只要左孩子，从下到上传递
        # 参数和返回值；返回左孩子的数值，传入的是节点
        # 停止条件：节点为空
        return self.traversal(root)
        
    def traversal(self, node:TreeNode):
        if not node:
            return 0
        lsum = self.traversal(node.left)
        # 左孩子不为空且左孩子没有孩子
        if node.left and not node.left.left and not node.left.right:
            lsum = node.left.val # 记录左孩子
        rsum = self.traversal(node.right)
        sums = lsum+rsum
        return sums
        
```
````
