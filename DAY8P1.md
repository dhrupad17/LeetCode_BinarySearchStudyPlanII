# Search a 2D Matrix II
---
- ## Question
---
>Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:
>
>- Integers in each row are sorted in ascending from left to right.
>- Integers in each column are sorted in ascending from top to bottom.
---
- ## Example
---
![alt text](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)
>Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
>
>Output: true
---
- ## Solution:
**Code :**
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row=0;
        int col=matrix[0].length-1;
        if(matrix==null|| matrix.length<0|| matrix[0].length<0)
            return false;
        while(col>=0 && row<matrix.length)
        {
            if(target==matrix[row][col])
                return true;
            else if( target< matrix[row][col])
            {
                col--;
            }
            else
                row++;
        }
        return false;
    }
}
