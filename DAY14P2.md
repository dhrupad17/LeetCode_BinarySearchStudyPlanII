# Shortest Subarray to be Removed to Make Array Sorted
---
- ## Question:
>Given an integer array arr, remove a subarray (can be empty) from arr such that the remaining elements in arr are non-decreasing.
>
>Return the length of the shortest subarray to remove.
>
>A subarray is a contiguous subsequence of the array.
---
- ## Example:
>Input: arr = [1,2,3,10,4,2,3,5]
>
>Output: 3
>
>Explanation: The shortest subarray we can remove is [10,4,2] of length 3. The remaining elements after that will be [1,2,3,3,5] which are sorted.
>Another correct solution is to remove the subarray [3,10,4].
---
- ## Solution:
**Code :**
```java
class Solution {
    public int findLengthOfShortestSubarray(int[] arr) {
        int low=0;
        int high=arr.length-1;
        for(;low<arr.length-1;low++)
        {
            if(arr[low]>arr[low+1])
                break;
        }
        if(low==arr.length-1)
            return 0;
        for(;high>0;high--)
        {
            if(arr[high]<arr[high-1])
                break;
        }
        int minlen=Math.min(arr.length-low-1,high);
        for(;low>=0;low--)
        {
            for(int i=high;i<arr.length;i++)
            {
                if(arr[low]>arr[i])
                    continue;
                minlen=Math.min(minlen,i-low-1);
                break;
            }
        }
        return minlen;
    }
}
