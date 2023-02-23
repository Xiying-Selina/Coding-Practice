# Day 23

## 669. Trim a Binary Search Tree

[link](https://leetcode.com/problems/trim-a-binary-search-tree/description/)

````python
//```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def trimBST(self, root: Optional[TreeNode], low: int, high: int) -> Optional[TreeNode]:
        # 终止条件
        if not root: return None
        # 小于low边界时，保存并返回删除后右子节点
        if root.val<low: return self.trimBST(root.right,low,high)
        # 大于high边界时，保存并返回删除后左子节点
        if root.val>high: return self.trimBST(root.left, low,high)
        root.left = self.trimBST(root.left, low,high)
        root.right = self.trimBST(root.right,low,high)
        return root

```
````

## 108. Convert Sorted Array to Binary Search Tree

[link](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        return self.traversal(nums,0,len(nums)-1)

    def traversal(self,nums,left,right):
        # 找根节点，切割区间
        if left>right: return None
        mid=left+(right-left)//2
        root=TreeNode(nums[mid])
        root.left=self.traversal(nums,left,mid-1)
        root.right=self.traversal(nums,mid+1,right)
        return root

```
````

## 538. Convert BST to Greater Tree

[link](https://leetcode.com/problems/convert-bst-to-greater-tree/description/)

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
        self.preval=0 #保留前一个结点的数值

    def convertBST(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        # 本题目右中左
        self.traversal(root)
        return root

    def traversal(self, cur:TreeNode):
        if not cur: return
        self.traversal(cur.right) #右
        cur.val+=self.preval
        self.preval=cur.val #中
        self.traversal(cur.left)


```
````
