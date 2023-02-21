# Day 20

## 654. Maximum Binary Tree

[link](https://leetcode.com/problems/maximum-binary-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        # 构造二叉树用前序遍历，最大的值设做根节点，分开左右子树
        # 停止条件：nums为空
        if not nums:
            return None
        # root的index和val
        root_val=max(nums)
        root_index=nums.index(root_val)
        root=TreeNode(root_val)
        # 切割nums为左右子树
        left = nums[:root_index]
        right = nums[root_index+1:]
        # 递归，看左右子树
        root.left=self.constructMaximumBinaryTree(left)
        root.right=self.constructMaximumBinaryTree(right)
        return root
```
````

## 617. Merge Two Binary Trees

[link](https://leetcode.com/problems/merge-two-binary-trees/submissions/901361066/)

```python
// # Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        # 终止条件：
        # 如果1为空则返回2，如果2为空则返回1
        if not root1: return root2
        if not root2: return root1
        # 前序遍历
        root1.val+=root2.val
        root1.left = self.mergeTrees(root1.left, root2.left)
        root1.right = self.mergeTrees(root1.right, root2.right)
        return root1
```

## 700. Search in a Binary Search Tree

[link](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        # 二叉搜索树，可以用层序遍历，利用其性质，不需要stack模拟
        while root:
            if root.val>val:
                root=root.left
            elif root.val<val:
                root=root.right
            else:
                return root
        return None

```
````

## 98. Validate Binary Search Tree

[link](https://leetcode.com/problems/validate-binary-search-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:

    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        # 此题层序遍历没有700好用，因为无法利用二叉搜索树特性，可以使用中序遍历
        # BST：中序遍历时形成单调递增数列
        pre=None # 存储遍历过的节点
        def __isValidBST(root: TreeNode) -> bool: 
            nonlocal pre
            # 停止条件：树为空
            if not root: return True
            # 左中右
            left = __isValidBST(root.left)
            if pre and pre.val>=root.val:
                return False
            pre=root #更新pre
            right = __isValidBST(root.right)
            return left and right
        return __isValidBST(root)


```
````
