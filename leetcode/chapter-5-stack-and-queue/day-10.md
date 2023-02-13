# Day 10

## 232. Implement Queue using Stacks

[Link](https://leetcode.com/problems/implement-queue-using-stacks/)

````python
// ```python3
class MyQueue:

    def __init__(self):
        # in 负责push；out 负责pop
        self.stack_in = []
        self.stack_out = []

    def push(self, x: int) -> None:
        # Pushes element x to the back of the queue.
        # 新元素进来时，放入stack_in
        self.stack_in.append(x)

    def pop(self) -> int:
        # Removes the element from the front of the queue and returns it.
        if self.empty():
            return None
        # 如果输出栈不为空，则直接从出栈弹出数据就可以了
        if self.stack_out:
            return self.stack_out.pop()
        else:
            # 输出栈如果为空，就把进栈数据全部导入进来
            for i in range(len(self.stack_in)):
                self.stack_out.append(self.stack_in.pop())
        return self.stack_out.pop()

    def peek(self) -> int:
        # Returns the element at the front of the queue.
        ans = self.pop()
        self.stack_out.append(ans)
        return ans

    def empty(self) -> bool:
        # Returns true if the queue is empty, false otherwise.
        # 如果进栈和出栈都为空的话，说明模拟的队列为空了
        if self.stack_in or self.stack_out:
            return False
        else:
            return True


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```
````

## 225. Implement Stack using Queues

[Link](https://leetcode.com/problems/implement-stack-using-queues/description/)

````python
// ```python3
class MyStack:

    def __init__(self):
        # in存放所有数据，out只有pop用到
        self.queue_in = deque()
        self.queue_out = deque()
        
    def push(self, x: int) -> None:
        self.queue_in.append(x)

    def pop(self) -> int:
        if self.empty():
            return None
        for i in range(len(self.queue_in)-1):
            self.queue_out.append(self.queue_in.popleft())
        # 交换in和out,其实可以只用一个queue实现
        # for i in range(len(self.queue_in)-1):
        #   self.queue_in.append(self.queue_in.popleft())
        # return self.queue_in.popleft()
        self.queue_in, self.queue_out = self.queue_out, self.queue_in    
        return self.queue_out.popleft()

    def top(self) -> int:
        # 仅有in会存放数据，所以返回第一个即可
        return self.queue_in[-1]

    def empty(self) -> bool:
        # 只有in存了数据
        if self.queue_in:
            return False
        else:
            return True


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```
````
