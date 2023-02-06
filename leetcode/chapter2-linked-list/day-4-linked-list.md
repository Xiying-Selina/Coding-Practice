# Day 4: Linked List

## 24. Swap Nodes in Pairs

[Link](https://leetcode.com/problems/swap-nodes-in-pairs/)

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        #虚拟头指针指向head，假设为0
        cur = dummy_head
        # 因为一次移动两个单位，None条件要注意
        while cur.next!=None and cur.next.next!=None:
            # step1: 断开dummy0和1 的连接，将dummy0指向2
            temp1 = cur.next.next.next #存放指向3
            temp2 = cur.next #存放指向1
            cur.next = cur.next.next#将dummy0指向2
            # step2: 断开1和2的连接，将2指向1
            cur.next.next = temp2 #将2指向1
            # step3：断开2和3的连接，将1指向3
            temp2.next = temp1
            # step4：cur向后移动2个位置
            cur = cur.next.next
        return dummy_head.next # 新的头节点
```
````

## 19. Remove Nth Node From End of List

[Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        # 双指针用法，fast先行，之后通过slow缩减区间
        fast = dummy_head
        slow = dummy_head
        # fast和slow保持的相对位置不变，当fast到尾端，slow走到倒数Nth位置
        # 相对位置差n，fast先走n步
        for _ in range(n):
            fast = fast.next
        # slow和fast一起移动，fast到尾端时停止
        while( fast.next!=None ):
            fast = fast.next
            slow = slow.next
        # 此时slow.next既需要删除的元素
        slow.next = slow.next.next
        return dummy_head.next

```
````

## 160. Intersection of Two Linked Lists

[Link](https://leetcode.com/problems/intersection-of-two-linked-lists/)

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        # 思路：从交点开始，尾部链表重合，即尾端对齐
        # 与移除倒数Nth元素的快慢指针类似，两个指针的相对位置不变
        # 相对位置相差为两个链表的长度差
        # 两个链表的长度
        def ListLen(head: ListNode) -> int:
            length = 0
            cur = head
            while cur.next!=None:
                length+=1
                cur=cur.next
            return length

        lenA = ListLen(headA)
        lenB = ListLen(headB)
        # 用long_head记录较长的链表，short_head记录较短的
        if lenA > lenB:
            long_cur, short_cur = headA ,headB 
            long_len, short_len = lenA, lenB
        else:
            long_cur, short_cur = headB ,headA 
            long_len, short_len = lenB, lenA
        # 先移动长链表的指针，使得尾部对齐
        # A和B的长度差，也就是相对位置
        for _ in range(long_len - short_len):
            long_cur = long_cur.next
        # 同时移动长短链表的指针
        while long_cur != None:
            # 当两个指针指向的位置相同时，返回节点
            if long_cur == short_cur:
                return long_cur
            else:
                long_cur = long_cur.next
                short_cur = short_cur.next
        return None

```
````

## 142. Linked List Cycle II

[Link](https://leetcode.com/problems/linked-list-cycle-ii/description/)

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 双指针，每一次移动fast+2而slow+1
        # fast和slow会相遇，说明fast比slow多走n圈
        # x:非环形部分长度； y: 入口到相遇的环形部分； z:相遇点到入口的环形部分
        # fast = x+y+n(y+z); slow = x+y
        # x+y+n(y+z)=2* (x+y) -> x=(n-1)(y+z)+z
        # if n=1 x=z; 此时，fast比slow多走一圈
        # x=z表示从head到环形入口的距离与从相遇点到环形入口的距离一致
        fast = head
        slow = head
        # 找相遇点
        while fast!=None and fast.next!=None:
            fast = fast.next.next
            slow = slow.next
            # 在相遇点停下，重建指针，找入口
            if fast ==slow:
                point1 = head #从head出发，到入口处，走x
                point2 = fast #从相遇点出发，到入口处，走z
                while point1 != point2:
                    point1=point1.next
                    point2=point2.next
                return point1
        return None

        
```
````
