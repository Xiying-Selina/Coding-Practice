# Day 14: 递归遍历

```python
// class TreeNode: 
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```

1. **确定递归函数的参数和返回值**
2. **确定终止条件**
3. **确定单层递归的逻辑**

## 144. Binary Tree Preorder Traversal

[Link](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = [] # 保存结果
        # preorder前序遍历：中左右
        def traversal(root:TreeNode):
            if root==None:
                return
            res.append(root.val) # 中
            traversal(root.left) # 左
            traversal(root.right) # 右
            return res
        traversal(root)
        return res
```
````

## 145. Binary Tree Postorder Traversal

[Link](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/897478285/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        # postorder后序遍历：左右中
        def traversal(root:TreeNode):
            if root==None:
                return
            traversal(root.left) #左
            traversal(root.right) #右
            res.append(root.val) #中
        traversal(root)
        return res
```

## 94. Binary Tree Inorder Traversal

[Link](https://leetcode.com/problems/binary-tree-inorder-traversal/submissions/897479302/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res=[]
        # inorder中序遍历：左中右
        def traversal(root:TreeNode):
            if root==None:
                return
            traversal(root.left) #左
            res.append(root.val) #中
            traversal(root.right) #右
        traversal(root)
        return res
            
```
