# Maximum Side Length of a Square with Sum Less than or Equal to Threshold
---
- ## Question:
>Given a m x n matrix mat and an integer threshold, return the maximum side-length of a square with a sum less than or equal to threshold or return 0 if there is no such square.
---
- ## Example:
![alt text](https://assets.leetcode.com/uploads/2019/12/05/e1.png)
>Input: mat = [[1,1,3,2,4,3,2],[1,1,3,2,4,3,2],[1,1,3,2,4,3,2]], threshold = 4
>
>Output: 2
>
>Explanation: The maximum side length of square with sum less than 4 is 2 as shown.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int maxSideLength(int[][] mat, int threshold) {
        int m=mat.length;
        int n=mat[0].length;
        int prefixsum[][]=new int[m+1][n+1];
        
        for(int i=1;i<=m;i++)
        {   int sum=0;
            for(int j=1;j<=n;j++)
            {
                sum=sum+mat[i-1][j-1];
                prefixsum[i][j]=prefixsum[i-1][j]+sum;
            }
        }
        for(int k=Math.min(m,n)-1;k>0;k--)
        {
            for(int i=1;i+k<=m;i++)
            {
                for(int j=1;j+k<=n;j++)
                {
                    if(prefixsum[i+k][j+k]-prefixsum[i-1][j+k]-prefixsum[i+k][j-1]+prefixsum[i-1][j-1]<=threshold)
                        return k+1;
                }
            }
        }
        return 0;
    }
}
