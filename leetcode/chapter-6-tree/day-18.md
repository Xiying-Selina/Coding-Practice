# Day 18

## 513. Find Bottom Left Tree Value

[link](https://leetcode.com/problems/find-bottom-left-tree-value/description/)

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
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        # 层序遍历: 位置上最左而不是左子树
        res=0
        if not root:
            return 0
        que=deque([root])
        while que:
            size=len(que)
            for i in range(size):
                cur=que.popleft()
                # 记录的是最后一层的第一个数字
                if i==0:
                    res=cur.val
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
        return res

```
````

## 112. Path Sum

[link](https://leetcode.com/problems/path-sum/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        # 前序遍历，每次target减去当前值，当遍历到叶子节点==0，则返回True
        return self.PathSum(root, targetSum)
        
    def PathSum(self, node, target):
        if not node:
            return False
        # 中：叶子节点且此时target被减到0，返回True
        if not node.left and not node.right and target-node.val==0:
            return True 
        # 其他叶子节点，返回False
        elif not node.left and not node.right:
            return False
        # 左右：每一层target会减去遍历过的值
        if self.PathSum(node.left, target-node.val): return True
        if self.PathSum(node.right, target-node.val): return True
        return False
```
````

## 113. Path Sum II

[link](https://leetcode.com/problems/path-sum-ii/submissions/900635961/)

```python
//# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        # 同105，前序遍历，每次target减去当前值，当遍历到叶子节点==0，则加入该路径
        # 需要res记录结果，path记录每个路径
        # 要遍历整个树，找到所有路径，所以递归函数不要返回值！
        res=[]
        path=[]
        self.PathSum(root, targetSum,path,res)
        return res
        
    def PathSum(self, node, target,path,res):
        if not node:
            return
        path.append(node.val) #记录节点
        # 中：叶子节点且此时target被减到0，则把该路径加入res
        if not node.left and not node.right and target-node.val==0:
            res.append(list(path)) 
        # 其他叶子节点，返回
        else: 
        # 左右：每一层target会减去遍历过的值
            self.PathSum(node.left, target-node.val,path,res)
            self.PathSum(node.right, target-node.val,path,res)
        path.pop()
```

## 106. Construct Binary Tree from Inorder and Postorder Traversal&#x20;

[link](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        # inorder: parent, lchild, rchild;
        # postorder: lchild, rchild, parent;
        # 终止条件：postorder为None
        if not postorder:
            return 
        # root：为postorder[-1]
        root_val = postorder[-1]
        root = TreeNode(root_val)
        # 用根节点切割inorder，左右部分分别构成左右子树
        root_index = inorder.index(root_val)
        left_inorder = inorder[:root_index]
        right_inorder = inorder[root_index+1:]
        # 用inorder得到的左右子树切割postorder，左右部分分别构成左右子树
        # 用长度切割，左右子树长度一定对应
        left_postorder=postorder[:len(left_inorder)]
        right_postorder=postorder[len(left_inorder):len(postorder)-1]
        # 递归，看左右子树
        root.left = self.buildTree(left_inorder, left_postorder)
        root.right = self.buildTree(right_inorder, right_postorder)
        return root


```
````

## 105. Construct Binary Tree from Preorder and Inorder Traversal

[link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        # inorder: parent, lchild, rchild;
        # preorder: parent,lchild, rchild;
        # 终止条件：preorder为None
        if not preorder:
            return 
        # root：为postorder[0]
        root_val = preorder[0]
        root = TreeNode(root_val)
        # 用根节点切割inorder，左右部分分别构成左右子树
        root_index = inorder.index(root_val)
        left_inorder = inorder[:root_index]
        right_inorder = inorder[root_index+1:]
        # 用inorder得到的左右子树切割preorder，左右部分分别构成左右子树
        # 用长度切割，左右子树长度一定对应
        left_preorder=preorder[1:1+len(left_inorder)]
        right_preorder=preorder[1+len(left_inorder):]
        # 递归，看左右子树
        root.left = self.buildTree(left_preorder,left_inorder)
        root.right = self.buildTree(right_preorder,right_inorder)
        return root
```
````
