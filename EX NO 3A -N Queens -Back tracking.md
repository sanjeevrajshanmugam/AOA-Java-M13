
# EX 3A N Queens Problem - Backtracking Approach.

## AIM:
To Write a Java program for N queens using backtracking approach.
You are given an integer N. For a given N x N chessboard, find a way to place 'N' queens such that no queen can attack any other queen on the chessboard.
A queen can be attacked when it lies in the same row, column, or the same diagonal as any of the other queens. You have to print one such configuration.
Chess Board
<img width="241" height="209" alt="image" src="https://github.com/user-attachments/assets/96aacb61-4f34-423f-b324-5e34454e42b8" />


Note :

Get the input from the user for N . The value of N must be from 1 to 4

If solution exists Print a binary matrix as output that has 1s for the cells where queens are placed

If there is no solution to the problem  print  "Solution does not exist"

## Algorithm
1. Initialize an N × N chessboard with all elements as 0.
2. Place queens column by column starting from column 0.
3. For each column:
Try placing a queen in each row one by one.
Check safety using the isSafe() function:
No queen in the same row (left side).
No queen in the upper-left diagonal.
No queen in the lower-left diagonal.
4.  If a position is safe, place the queen (board[i][col] = 1) and recur for the next column.
5.  If placing in the current column fails, backtrack — remove the queen (board[i][col] = 0) and try next row.
6.  If all queens are placed successfully, print the board as a valid solution.
7.  If no configuration works, print “Solution does not exist.”

## Program:
```

Developed by: SANJEEV RAJ S
Register Number: 212223220096
import java.util.Scanner;

public class NQueens {
    static int N;

    
    static void printSolution(int[][] board) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    
    static boolean isSafe(int[][] board, int row, int col) {
  
        for (int i = 0; i < col; i++)
            if (board[row][i] == 1)
                return false;

       
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
            if (board[i][j] == 1)
                return false;

        
        for (int i = row, j = col; i < N && j >= 0; i++, j--)
            if (board[i][j] == 1)
                return false;

        return true;
    }


    static boolean solveNQUtil(int[][] board, int col) {
        if(col>=N)
            return true;
        for(int i=0;i<N;i++){
            if(isSafe(board,i,col)){
                board[i][col]=1;
                if(solveNQUtil(board,col+1))
                return true;
                board[i][col]=0;
            }
        }
        return false;
       
    }

    
    static boolean solveNQ() {
        int[][] board = new int[N][N];

        if (!solveNQUtil(board, 0)) {
            System.out.println("Solution does not exist");
            return false;
        }

        printSolution(board);
        return true;
    }

   
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt(); 
        solveNQ();
    }
}


```

## Output:
<img width="676" height="295" alt="image" src="https://github.com/user-attachments/assets/82f0c38f-1e4f-47bd-9bc5-dae636176df6" />



## Result:
The program successfully implemented and the ouput is verified. 
