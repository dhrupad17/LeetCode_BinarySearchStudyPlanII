# Valid Triangle Number
---
- ## Question:
>Given an integer array nums, return the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.
---
- ## Example:
>Input: nums = [2,2,3,4]
>
>Output: 3
>
>Explanation: Valid combinations are: 
>
> 2,3,4 (using the first 2)
> 
> 2,3,4 (using the second 2)
> 
> 2,2,3
---
- ## Solution:
**Code :**
```java
class Solution {
    public int triangleNumber(int[] nums) {
        Arrays.sort(nums);
       int i;
       int count=0; 
       for(i=nums.length-1;i>=1;i--)
       {
           int right=i-1;
           int left=0;
           while(left<right)
           {
               if(nums[left]+nums[right]>nums[i])
               {
                   count=count+right-left;
                   right--;
               }
               else
               {
                   left++;
               }
           }
       }
        return count;
    }
}
