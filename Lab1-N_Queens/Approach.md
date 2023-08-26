# Solution to solve N queen problem can be via: 
## 1. Backtracking

According to Wikipedia, "Backtracking can be defined as a general algorithmic technique that considers searching every possible combination in order to solve a computational problem."
Initially, we start the backtracking from one possible option and if the problem is solved with that selected option then we return the solution else we backtrack and select another option from the remaining available options. There also might be a case where none of the options will give you the solution and hence we understand that backtracking won’t give any solution to that particular problem. We can also say that backtracking is a form of recursion. This is because the process of finding the solution from the various option available is repeated recursively until we don’t find the solution or we reach the final state. 

There are three types of problems in backtracking –  
Decision Problem – In this, we search for a feasible solution.
Optimization Problem – In this, we search for the best solution.
Enumeration Problem – In this, we find all feasible solutions.

### For this lab assignment, our question falls under the type of an Enumeration Problem as we have to find all the possible ways N queens can be placed in a NxN chessboard. 

Code is as follows:
``` 
global N
N = 4
def printSolution(board):
    for i in range(N):
        for j in range(N):
            print (board[i][j],end=' ')
        print()
 
def isSafe(board, row, col):
    # Check this row on left side
    for i in range(col):
        if board[row][i] == 1:
            return False
 
    # Check upper diagonal on left side
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
 
    # Check lower diagonal on left side
    for i, j in zip(range(row, N, 1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
 
    return True
 
def solveNQUtil(board, col):
    if col >= N:
        return True
 
    for i in range(N):
 
        if isSafe(board, i, col):
            # Place this queen in board[i][col]
            board[i][col] = 1
 
            # recur to place rest of the queens
            if solveNQUtil(board, col + 1) == True:
                return True
 
            # If placing queen in board[i][col
            # doesn't lead to a solution, then
            # queen from board[i][col]
            board[i][col] = 0
    return False

def solveNQ():
    board = [ [0, 0, 0, 0],
              [0, 0, 0, 0],
              [0, 0, 0, 0],
              [0, 0, 0, 0]
             ]
 
    if solveNQUtil(board, 0) == False:
        print ("Solution does not exist")
        return False
 
    printSolution(board)
    return True
solveNQ()
```

## 2. A star algorithm