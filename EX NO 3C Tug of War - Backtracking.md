
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
Register Number:212223220096

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
