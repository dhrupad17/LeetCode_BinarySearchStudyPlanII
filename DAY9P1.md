# Frequency of the Most Frequent Element
---
- ## Question:
>The frequency of an element is the number of times it occurs in an array.
>
>You are given an integer array nums and an integer k. In one operation, you can choose an index of nums and increment the element at that index by 1.
>
>Return the maximum possible frequency of an element after performing at most k operations.
---
- ## Example:
>Input: nums = [1,2,4], k = 5
>
>Output: 3
>
>Explanation: Increment the first element three times and the second element two times to make nums = [4,4,4].
>4 has a frequency of 3.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int maxFrequency(int[] nums, long k) {
        Arrays.sort(nums);
        int i=0;
        int j;
        for(j=0;j<nums.length;j++)
        {
            k=k+nums[j];
            if(k<(long)(nums[j]*(j-i+1)))
            {
                k=k-nums[i++];
            }
        }
        return j-i;
    }
}
