# Longest Increasing Subsequence
---
- ## Question
---
>Given an integer array nums, return the length of the longest strictly increasing subsequence.
>
>A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].
---
- ## Example
---
>Input: nums = [10,9,2,5,3,7,101,18]
>
>Output: 4
>
>Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len=0;
       int dp[]=new int[nums.length];
        for(int x:nums)
        {
            int i=Arrays.binarySearch(dp,0,len,x);
            if(i<0)
                i=-(i+1);
            dp[i]=x;
            if(i==len)
                len++;
        }
        return len;
    }
}
