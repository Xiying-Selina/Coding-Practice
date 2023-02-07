# Day 3: Linked List

```python
// 
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class MyLinkedList:

    def __init__(self):
        self.head = ListNode()
        self.size = 0
```

## 203. Remove Linked List Elements

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy_head = ListNode(next = head)
        cur = dummy_head
        while cur.next != None:
            if cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
        return dummy_head.next
```
````

## 707. Design Linked List

````python
// ```python3
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class MyLinkedList:

    def __init__(self):
        self.head = ListNode()
        self.size = 0

    def get(self, index: int) -> int:
        if index<0 or index>=self.size:
            return -1
        cur = self.head
        for i in range(index+1):
            cur=cur.next
        return cur.val

    def addAtHead(self, val: int) -> None:
        self.addAtIndex(0,val)
        
    def addAtTail(self, val: int) -> None:
        self.addAtIndex(self.size, val)

    def addAtIndex(self, index: int, val: int) -> None:
        if index>self.size:
            return 
        self.size+=1
        cur = self.head
        for i in range(index):
            cur = cur.next
        newnode = ListNode(val)
        newnode.next = cur.next
        cur.next = newnode
  
    def deleteAtIndex(self, index: int) -> None:
        if index<0 or index>=self.size:
            return 
        self.size-=1
        cur = self.head
        for i in range(index):
            cur = cur.next
        cur.next = cur.next.next


        

# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```
````

## 206. Reverse Linked List

````python
// ```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        pre = None
        while cur!=None:
            temp = cur.next # store the postion of cur.next
            cur.next = pre # change the direction
            pre = cur # move pre forward
            cur = temp # move cur forward
        return pre # pre presents the new linkedlist
            
```
````
