# Single Element in a Sorted Array
---
- ## Question:
>You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.
>
>Return the single element that appears only once.
>
>Your solution must run in O(log n) time and O(1) space.
---
- ## Example:
>Input: nums = [1,1,2,3,3,4,4,8,8]
>
>Output: 2
---
- ## Solution:
**Code :**
```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low=0;
        int high=nums.length-1;
        while(low<high)
        {
            int mid=low+(high-low)/2;
            if(nums[mid]==nums[mid+1])
                mid=mid-1;
            int left=mid-low+1;
            int right=high-mid;
            if(left%2!=0)
                high=mid;
            else
                low=mid+1;
        }
        return nums[low];
    }
}
