# Day 11: Application of stack

## 20. Valid Parentheses

[Link](https://leetcode.com/problems/valid-parentheses/description/)

````python
// ```python3
class Solution:
    def isValid(self, s: str) -> bool:
        # 一共有三种不匹配：1.左右不匹配；2.左有右无；3.左无右有
        # 用栈解决类似消除的操作，因为栈帮助我们记录了：
        # 遍历数组当前元素时候，前一个元素是什么
        stack = []
        # 解法：遇到左括号存放右括号，右括号时查找左括号
        for i in s:
            if i == "(": stack.append(")")
            elif i == "[": stack.append("]")
            elif i == "{": stack.append("}")
            # False情况：所需左括号不对应/最后stack里面多了存入的元素
            # stack为空，或者最后一位不对应
            elif not stack or stack[-1]!=i:
                return False
            else:
                stack.pop()
        # 最终的stack也必须为空，因为所有元素被pop
        return True if not stack else False

```
````

## 1047. Remove All Adjacent Duplicates In String

[Link](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/description/)

````python
// ```python3
class Solution:
    def removeDuplicates(self, s: str) -> str:
        # similar with 20.valid parentatheses
        stack=[]
        for i in s:
            if not stack or stack[-1]!=i:
                stack.append(i)
            else:
                stack.pop()
        return "".join(stack)
```
````

## 150. Evaluate Reverse Polish Notation

[Link](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

````python
// ```python3
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        # stack's application
        stack = []
        for i in tokens:
            # 将数字放入stack
            if i not in ["+","-","*","/"]:
                stack.append(int(i))
            # 遇到运算符号，pop两个数字进行运算，注意后进先出
            else:
                num2=stack.pop()
                num1=stack.pop()
                if i =="+": stack.append(num1+num2)
                if i =="-": stack.append(num1-num2)
                if i =="*": stack.append(num1*num2)
                if i =="/": stack.append(int(num1/num2))
        return stack[0]
```
````
