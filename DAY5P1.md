# Find the Duplicate Number
---
- ## Question
---
>Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.
>
>There is only one repeated number in nums, return this repeated number.
>
>You must solve the problem without modifying the array nums and uses only constant extra space.
---
- ## Example
---
>Input: nums = [1,3,4,2,2]
>
>Output: 2
---
- ## Solution:
**Code :**
```java
class Solution {
    public int findDuplicate(int[] arr) {
        int i=0;
        while(i<arr.length)
        {
            if(arr[i]!=i+1)
            {
            int index=arr[i]-1;
            if(arr[i]!=arr[index])
            {
                int temp=arr[i];
                arr[i]=arr[index];
                arr[index]=temp;
            }
            else
            {
                return arr[i];
            }
            }
            else
            {
                i++;
            }
        }
        return -1;
    }
}
