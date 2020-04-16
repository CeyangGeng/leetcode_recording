# N-Queens

- Description

  > The *n*-queens puzzle is the problem of placing *n* queens on an *n*×*n* chessboard such that no two queens attack each other.
  >
  > ![img](https://assets.leetcode.com/uploads/2018/10/12/8-queens.png)
  >
  > Given an integer *n*, return all distinct solutions to the *n*-queens puzzle.
  >
  > Each solution contains a distinct board configuration of the *n*-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.
  >
  > **Example:**
  >
  > ```python
  > Input: 4
  > Output: [
  >  [".Q..",  // Solution 1
  >   "...Q",
  >   "Q...",
  >   "..Q."],
  > 
  >  ["..Q.",  // Solution 2
  >   "Q...",
  >   "...Q",
  >   ".Q.."]
  > ]
  > Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above.
  > ```

- Solution: https://leetcode.com/problems/n-queens/discuss/19808/Accepted-4ms-c%2B%2B-solution-use-backtracking-and-bitmask-easy-understand.

  > 1. Backtracking: Every time when we put queen at a certain position, we must check the validness of this position first. If there is a queen at any position which is in the same row, the same colum, the across line(45°， 135°) with the position to be placed,  this position is invalid! We make the row as a parameter and iter on all the column from 0 to N.
  >
  >    ```python
  >    class Solution:
  >        def solveNQueens(self, n: int) -> List[List[str]]:
  >            res = []
  >            path = [['.' for _ in range(n)] for _ in range(n)]
  >            self.backtrack(res, path, 0, n)
  >            return res
  >        def backtrack(self, res, path, row, n):
  >            if row == n: 
  >                temp = []
  >                for i in range(n):
  >                    temp.append(''.join(path[i]))
  >                res.append(temp)
  >                return
  >            for col in range(n):
  >                if self.isvalid(row, col, path, n):
  >                    path[row][col] = 'Q'
  >                    self.backtrack(res, path, row + 1, n)
  >                    path[row][col] = '.'
  >        def isvalid(self, row, col, board, n):
  >            for i in range(n):
  >                if board[i][col] == 'Q':return False
  >            for j in range(n):
  >                if board[row][j] == 'Q': return False
  >            i, j = row, col
  >            while i >= 0 and j >= 0:
  >                if board[i][j] == 'Q': return False
  >                i, j = i - 1, j - 1
  >            i, j = row, col
  >            while i >= 0 and j < n:
  >                if board[i][j] == 'Q': return False
  >                i, j = i - 1, j + 1
  >            return True
  >    ```
  >
  > 2. Making use of the property of the sum of the indexes of the elements located at the main cross line and sub cross line. This idea is wonderful!
  >
  >    ```python
  >    class Solution:
  >        def solveNQueens(self, n: int) -> List[List[str]]:
  >            flag = [1] * (5 * n - 2)
  >            res = []
  >            board = [['.'] * n for _ in range(n)]
  >            self.backtrack(flag, res, board, 0, n)
  >            return res
  >        def backtrack(self, flag, res, board, row, n):
  >            if row == n:
  >                temp = []
  >                for i in range(n):
  >                    temp.append(''.join(board[i]))
  >                res.append(temp)
  >                return 
  >            for col in range(n):
  >                if flag[col] and flag[n + row + col] and flag[4 * n - 2 + row - col]:
  >                    flag[col] = flag[n + row + col] = flag[4 * n - 2 + row - col] = 0
  >                    board[row][col] = 'Q'
  >                    self.backtrack(flag, res, board, row + 1, n)
  >                    board[row][col] = '.'
  >                    flag[col] = flag[n + row + col] = flag[4 * n - 2 + row - col] = 1
  >                    
  >            
  >    ```
  >
  >    

