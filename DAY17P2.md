# Find a Peak Element II
---
- ## Question:
>A peak element in a 2D grid is an element that is strictly greater than all of its adjacent neighbors to the left, right, top, and bottom.
>
>Given a 0-indexed m x n matrix mat where no two adjacent cells are equal, find any peak element mat[i][j] and return the length 2 array [i,j].
>
>You may assume that the entire matrix is surrounded by an outer perimeter with the value -1 in each cell.
>
>You must write an algorithm that runs in O(m log(n)) or O(n log(m)) time.
---
- ## Example:
![alt text](https://assets.leetcode.com/uploads/2021/06/08/1.png)
>Input: mat = [[1,4],[3,2]]
>
>Output: [0,1]
>
>Explanation: Both 3 and 4 are peak elements so [1,0] and [0,1] are both acceptable answers.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int[] findPeakGrid(int[][] mat) {
        int m=mat.length;
        int n=mat[0].length;
        int left,right,top,bottom;
        int i=0,j=0;
        while(true)
        {
            int curr=mat[i][j];
            if(i==0)
                top=-1;
            else
                top=mat[i-1][j];
            if(i==m-1)
                bottom=-1;
            else
                bottom=mat[i+1][j];
            if(j==0)
                left=-1;
            else
                left=mat[i][j-1];
            if(j==n-1)
                right=-1;
            else
                right=mat[i][j+1];
            if(curr>top && curr>bottom && curr> left && curr>right)
                return new int[]{i,j};
            else
            {
                int mx=Math.max(top,Math.max(bottom,Math.max(left,right)));
                if(mx==top)
                    i=i-1;
                if(mx==bottom)
                    i=i+1;
                if(mx==left)
                    j=j-1;
                if(mx==right)
                    j=j+1;
            }
        }
    }
}
