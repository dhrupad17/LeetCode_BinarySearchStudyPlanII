# Find Peak Element
---
- ## Question
---
>A peak element is an element that is strictly greater than its neighbors.
>
>Given an integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.
>
>You may imagine that nums[-1] = nums[n] = -∞.
>
>You must write an algorithm that runs in O(log n) time.
---
- ## Example
---
> Input: nums = [1,2,3,1]
> 
> Output: 2
> 
> Explanation: 3 is a peak element and your function should return the index number 2.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int findPeakElement(int[] arr) {
        int start=0;
        int end=arr.length-1;
        while(start<end)
        {
            int mid= start+ (end-start)/2;
            if(arr[mid]>arr[mid+1])
            {
                end=mid;
            }
            else
            {
                start=mid+1;
            }
        }
        return start;
    }
}
