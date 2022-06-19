# Find Right Interval
---
- ## Question
>You are given an array of intervals, where intervals[i] = [starti, endi] and each starti is unique.
>
>The right interval for an interval i is an interval j such that startj >= endi and startj is minimized. Note that i may equal j.
>
>Return an array of right interval indices for each interval i. If no right interval exists for interval i, then put -1 at index i.
---
- ## Example 
>Input: intervals = [[1,2]]
>
>Output: [-1]
>
>Explanation: There is only one interval in the collection, so it outputs -1.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int[] findRightInterval(int[][] intervals) {
        int[] result=new int[intervals.length];
        for(int i=0;i<intervals.length;i++)
        {
            result[i]=search(intervals[i][1],intervals);
        }
        return result;
    }
    public int search(int num, int[][] intervals)
    {
        int idx=-1;
        int min=Integer.MAX_VALUE;
        for(int i=0;i<intervals.length;i++)
        {
            if(intervals[i][0]>=num && intervals[i][0]<min)
            {
                min=intervals[i][0];
                idx=i;
            }
        }
        return idx;
    }
}
