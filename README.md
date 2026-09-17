
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


# EX 3B Rat in Maze- Backtracking 

## AIM:
To write a Java program to for given constraints.
here is a ball in a maze with empty spaces (represented as 0) and walls (represented as 1). The ball can go through the empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the m x n maze, the ball's start position and the destination, where start = [startrow, startcol] and destination = [destinationrow, destinationcol], return true if the ball can stop at the destination, otherwise return false.

You may assume that the borders of the maze are all walls (see examples).
<img width="573" height="573" alt="image" src="https://github.com/user-attachments/assets/d6f1c054-cdc2-4bb3-9c55-512fb2cf0fb7" />
Input: maze = [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]], start = [0,4], destination = [4,4]
Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.


## Algorithm
1. Start the program and read the maze dimensions m and n.
2. Input the maze matrix (0 = open path, 1 = wall).
3. Read the start position and destination position.
4. Initialize a visited[m][n] boolean matrix to track visited cells.
5. Call the DFS function dfs(m, n, maze, start, destination, visited) to explore paths.  

## Program:
```

Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096
import java.util.*;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

 
        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] maze = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maze[i][j] = sc.nextInt();
            }
        }

       
        int[] start = new int[]{sc.nextInt(), sc.nextInt()};

        
        int[] destination = new int[]{sc.nextInt(), sc.nextInt()};

        Solution sol = new Solution();
        boolean result = sol.hasPath(maze, start, destination);

        System.out.println(result);
    }
}

class Solution {
    public boolean dfs(int m, int n, int[][] maze, int[] curr, int[] destination, boolean[][] visit) {
        if (visit[curr[0]][curr[1]]){
            return false;
        }
        if(curr[0]==destination[0]&&curr[1]==destination[1]){
            return true;
        }
        visit[curr[0]][curr[1]]=true;
        int[] dirX={0,1,0,-1};
        int[] dirY={-1,0,1,0};
        for(int i=0;i<4;i++){
            int r=curr[0],c=curr[1];
            while(r>=0&&r<m&&c>=0&& c<n&&maze[r][c]==0){
                r+=dirX[i];
                c+=dirY[i];
            }
            r-=dirX[i];
            c-=dirY[i];
            if(dfs(m,n,maze,new int[]{r,c},destination,visit)){
                return true;
            }
        }
        return false;
    }
        
        
    public boolean hasPath(int[][] maze,int[] start,int[] destination){
        int m=maze.length;
        int n=maze[0].length;
        boolean[][] visit=new boolean[m][n];
        return dfs(m,n,maze,start,destination,visit);
    }
    
}


```

## Output:

<img width="444" height="548" alt="image" src="https://github.com/user-attachments/assets/094f1c2c-35d5-4976-b4c6-77c5763e78ea" />


## Result:
The program successfully implemented and the expected output is verified.


# EX 3C Tug of War problem - Backtracking.

## AIM:
To write a Java program to for given constraints.
Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.

## Algorithm
1. Start the program and read the number of elements n and the array nums[].
2. Compute the total sum of all elements in the array.
If the total sum is odd, return false (it cannot be divided equally).
3. Calculate the target subset sum as subSetSum = totalSum / 2.
The goal is to determine if there exists a subset whose sum equals subSetSum. 
4.  Initialize a boolean DP array dp[subSetSum + 1] where
dp[i] indicates whether a subset with sum i can be formed.
Set dp[0] = true (sum 0 is always possible with an empty subset).
5. For each number curr in nums[]:
Traverse dp[] backward from subSetSum down to curr:
Update dp[j] = dp[j] || dp[j - curr].
6. After processing all numbers, check dp[subSetSum]:
If true, print true (array can be partitioned into two equal subsets).
Else, print false.

## Program:
```

Developed by: SANJEEV RAJ S
Register Number: 212223220096

import java.util.Scanner;
public class Solution {
    public boolean canPartition(int[] nums) {
        if(nums.length==0)
            return false;
        int totalSum=0;
        for(int num:nums){
            totalSum+=num;
        }
        if (totalSum%2!=0)
            return false;
        int subSetSum=totalSum/2;
        boolean[] dp=new boolean[subSetSum+1];
        dp[0]=true;
        for(int curr:nums){
            for(int j=subSetSum;j>=curr;j--){
                dp[j]|=dp[j-curr];
            }
        }
        return dp[subSetSum];
        
        
        
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution sol = new Solution();
        int n = scanner.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }
        boolean canBePartitioned = sol.canPartition(nums);
        System.out.println(canBePartitioned);
    }
}


```

## Output:
<img width="535" height="253" alt="image" src="https://github.com/user-attachments/assets/f6430429-a703-42b6-a7f0-cc52fd150f61" />



## Result:
The program successfully implemented and the expected output is verified.


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
Register Number: 212223220096
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


# EX 3E Generate Permutations using Backtracking  Approach.

## AIM:
To write a Java program to for given constraints.
Given an array nums of distinct integers, return all the possible Permutation. You can return the answer in any order.

## Algorithm
1. Input Processing:
Read the array elements from user input, remove brackets ([]), split by commas, and store them in an integer array nums.
2. Start Permutation Generation:
Initialize an empty list ans to store all permutations and call the recursive backtrack() function with an initially empty list curr.
3. Recursive Backtracking Logic:
If curr (the current permutation) has the same length as nums, add a copy of curr to ans.
Otherwise, iterate through each number in nums.
4.  Build and Explore Permutations:
For each number not already in curr, add it to curr, recursively call backtrack() to build further, and then remove it (backtrack) to explore other possibilities.
5.  Output Result:
After recursion completes, print all generated permutations stored in ans. 

## Program:
```
Developed by: SANJEEV RAJ S
Register Number: 212223220096
import java.util.*;

public class Solution {

    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(new ArrayList<>(), ans, nums);
        return ans;
    }

    public void backtrack(List<Integer> curr, List<List<Integer>> ans, int[] nums) {
        if (curr.size() == nums.length) {
            ans.add(new ArrayList<>(curr));
            return;
        }
        for (int num : nums) {
            if (!curr.contains(num)) {
                curr.add(num);
                backtrack(curr, ans, nums);
                curr.remove(curr.size() - 1);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String inputLine = scanner.nextLine().trim();

        inputLine = inputLine.replaceAll("\\[|\\]", "");
        String[] parts = inputLine.split(",");

        int[] nums = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }

        Solution solution = new Solution();
        List<List<Integer>> permutations = solution.permute(nums);
        System.out.println(permutations);
        scanner.close();
    }
}
 

```

## Output:
<img width="1246" height="239" alt="image" src="https://github.com/user-attachments/assets/45b05d0f-2a94-4edc-9b76-4492737efec6" />

## Result:
The program successfully implemented and the expected output is verified.
