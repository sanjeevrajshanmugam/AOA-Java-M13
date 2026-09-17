
# EX 3D Sudoku solver - Backtracking.

## AIM:
To write a Java program to solve a Sudoku puzzle by filling the empty cells.


## Algorithm
1. Start the program and read the 9×9 Sudoku board.
Empty cells are represented by 0.
2. Define a function isSafe(board, row, col, num) to check if placing num in position (row, col) is valid:
Check that num does not already exist in the same row.
Check that num does not already exist in the same column.
Check that num does not exist in the 3×3 subgrid containing (row, col).
Return true if all checks pass; otherwise, return false.
3. Define a recursive function solveSudoku(board, row, col):
If (row == 8 && col == 9), all cells are filled → return true (solution found).
If col == 9, move to the next row (row + 1) and set col = 0.
If the current cell is already filled (non-zero), call solveSudoku for the next column.
For an empty cell (0):
Try placing numbers 1 through 9:
If isSafe() returns true, temporarily place the number.
Recursively call solveSudoku() for the next cell.
If recursion succeeds, return true.
If not, backtrack by resetting the cell to 0.
If no number can be placed, return false.
4. In the main() method:
Input the Sudoku grid from the user.
Call solveSudoku(board, 0, 0).
If it returns true, print the solved Sudoku grid using printBoard().
Otherwise, print “No solution exists.”
5. End the program.  

## Program:
```
Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.Scanner;

public class SudokuSolver {

    
    static boolean isSafe(int[][] board, int row, int col, int num) {
       
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num)
                return false;
        }

       
        int startRow = row - row % 3;
        int startCol = col - col % 3;

        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[startRow + i][startCol + j] == num)
                    return false;

        return true;
    }

   
    static boolean solveSudoku(int[][] board, int row, int col) {
        if(row==8&&col==9)
            return true;
        if(col==9){
            row++;
            col=0;
        }
        if(board[row][col]!=0)
            return solveSudoku(board,row,col+1);
        for(int num=1;num<=9;num++){
            if(isSafe(board,row,col,num)){
                board[row][col]=num;
                if(solveSudoku(board,row,col+1))
                    return true;
                board[row][col]=0;
            }
        }
        return false;
    }

   
    static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] board = new int[9][9];

      

        for (int i = 0; i < 9; i++) {
            
            for (int j = 0; j < 9; j++) {
                board[i][j] = sc.nextInt();
            }
        }

      

        if (solveSudoku(board, 0, 0)) {
            System.out.println("Solved Sudoku:");
            printBoard(board);
        } else {
            System.out.println("No solution exists.");
        }

        sc.close();
    }
}


```

## Output:
<img width="670" height="621" alt="image" src="https://github.com/user-attachments/assets/c914410d-005a-40e6-ae09-ad5897cb6202" />



## Result:
The program successfully implemented and the expected output is verified.
