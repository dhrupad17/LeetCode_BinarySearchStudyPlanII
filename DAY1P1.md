# Minimum Size Subarray Sum
---
- ## Question:
>Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. 
>If there is no such subarray, return 0 instead.

---
- ## Example:
> Input: target = 7, nums = [2,3,1,2,4,3]
> 
> Output: 2
> 
> Explanation: The subarray [4,3] has the minimal length under the problem constraint.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int i=0;
        int j=0;
        int sum=0;
        int min=Integer.MAX_VALUE;
        if(nums.length==0 || nums==null)
            return 0;
        while(j<nums.length)
        {
            sum=sum+nums[j++];
            while(sum>=target)
            {
                min=Math.min(min,j-i);
                sum=sum-nums[i++];
            }
        }
        if(min==Integer.MAX_VALUE)
            return 0;
        else
            return min;
    }
}
