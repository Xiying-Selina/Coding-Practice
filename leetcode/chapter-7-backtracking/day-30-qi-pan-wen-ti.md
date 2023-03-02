# Day 30: 棋盘问题

## 51. N-Queens

[link](https://leetcode.com/problems/n-queens/description/)

````python
// ```python3
class Solution:
    def __init__(self):
        self.res = []
        

    def solveNQueens(self, n: int) -> List[List[str]]:
        board = [["."] *n for _ in range(n)]
        self.backtracking(board,n,0)
        return self.res

    def isValid(self, row, col, board):
        # 判断在board[row][col]放入"Q"是否合法（列，对角线）
        # 行上因为每层递归已经保证不重复，不需要再次判断
        for i in range(len(board)): # 检查每一列
            if board[i][col] =="Q": return False
        i, j = row-1, col-1  
        while i >=0 and j>=0: # 检查左上角
            if board[i][j] =="Q": return False
            i-=1
            j-=1
        i, j = row-1, col+1  
        while i>=0 and j<len(board): # 检查右上角
            if board[i][j] =="Q": return False
            i-=1
            j+=1
        return True

    def backtracking(self,board, n,row):
        # row记录每次递归的行数，到叶子节点收集棋盘结果
        if row==n: 
            board_lst = []
            for line in board:
                line_str = "".join(line)
                board_lst.append(line_str)
            self.res.append(board_lst)
            return
        # 单层递归，此时i为列数，row为行数
        for i in range(n):
            # 处理节点，判断填入Q的合法性
            if self.isValid(row, i, board):
                board[row][i]="Q"
                self.backtracking(board,n,row+1)
                board[row][i]="."

```
````

## 37. Sudoku Solver

[link](https://leetcode.com/problems/sudoku-solver/description/)

````python
// ```python3
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        self.backtracking(board)

    def isValid(self, row:int,col:int,num:int, board: List[List[str]]) -> bool:
        # 判断同一行是否冲突
        for i in range(9):
            if board[row][i]==str(num): return False
        # 判断同一列是否冲突
        for j in range(9):
            if board[j][col]==str(num): return False
        # 判断同一九宫格是否有冲突
        subrow, subcol = (row // 3) * 3, (col // 3) * 3
        for i in range(subrow, subrow+3):
            for j in range(subcol, subcol+3):
                if board[i][j]==str(num): return False
        return True

    def backtracking(self, board: List[List[str]]) -> bool:
        # 因为只需要返回一个结果，可以用bool，只要true就返回
        # 需要两层循环，一层行，一层列
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] != ".": continue #非空白处tiaoguo
                for k in range(1,10):
                    # 判断每次填写合法性
                    if self.isValid(i,j,k,board):
                        board[i][j] = str(k)
                        if self.backtracking(board): return True
                        board[i][j] = "."
                # 若数字1-9都不能成功填入空格，返回False无解
                return False
        # 若棋盘填满，返回true
        return True
                


```
````

## 332. Reconstruct Itinerary

link

```python
// Some code
```
