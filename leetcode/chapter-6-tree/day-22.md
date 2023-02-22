# Day 22

## 235. Lowest Common Ancestor of a Binary Search Tree

[link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

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
        # 同236，但可以用BST特性
        # 层序遍历
        cur=root
        while cur:
            if cur.val>p.val and cur.val>q.val:
                cur=cur.left
            elif cur.val<p.val and cur.val<q.val:
                cur=cur.right
            else:
                return cur
```
````

## 701. Insert into a Binary Search Tree

[link](https://leetcode.com/problems/insert-into-a-binary-search-tree/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        # BST：插入节点一定在叶子节点
        # 将新的node传到上层
        if not root: 
            node=TreeNode(val)
            return node
        if val<root.val:
            root.left = self.insertIntoBST(root.left,val)
        if val>root.val:
            root.right = self.insertIntoBST(root.right, val)
        return root
```
````

## 450. Delete Node in a BST

[link](https://leetcode.com/problems/delete-node-in-a-bst/description/)

````python
// ```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        # 每一次return被删除节点的下一个节点
        # 情况一：找不到元素
        if not root: return None
        if root.val==key:
            # 情况二：删除叶子节点
            if not root.left and not root.right:
                return None
            # 情况三：左节点空或右节点空
            elif root.left and not root.right:
                return root.left
            elif not root.left and root.right:
                return root.right
            # 情况四：左右节点都不为空
            else:
                # cur记录右节点的左孩子，删除节点后，把左子树整个加入到右节点左孩子下
                cur=root.right 
                while cur.left:
                    cur=cur.left
                cur.left=root.left
                # 此时左边为空
                return root.right
        if key<root.val: root.left = self.deleteNode(root.left, key)
        if key>root.val: root.right = self.deleteNode(root.right, key)
        return root
                

```
````
