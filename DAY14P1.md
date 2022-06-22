# Range Sum of Sorted Subarray Sums
---
- ## Question:
>You are given the array nums consisting of n positive integers. You computed the sum of all non-empty continuous subarrays from the array and then sorted them in non-decreasing order, creating a new array of n * (n + 1) / 2 numbers.
>
>Return the sum of the numbers from index left to index right (indexed from 1), inclusive, in the new array. Since the answer can be a huge number return it modulo 109 + 7.
---
- ## Example:
>Input: nums = [1,2,3,4], n = 4, left = 1, right = 5
>
>Output: 13 
>
>Explanation: All subarray sums are 1, 3, 6, 10, 2, 5, 9, 3, 7, 4. After sorting them in non-decreasing order we have the new array [1, 2, 3, 3, 4, 5, 6, 7, 9, 10]. The sum of the numbers from index le = 1 to ri = 5 is 1 + 2 + 3 + 3 + 4 = 13. 
---
- ## Solution:
**Code :**
```java
class Solution {
    public int rangeSum(int[] nums, int n, int left, int right) {
        int index = 0;
        int[] sums = new int[n*(n+1)/2];
        
        for(int i = 0; i < n; i++) {
            int sum = 0;
            for(int j = i; j < n; j++) {
                sum += nums[j];
                sums[index++] = sum;
            }
        }
        
        int res = 0, mod = 1000000007;
        Arrays.sort(sums);
        for(int i = left-1; i < right; i++) {
            res = (res+sums[i])%mod;
        }
        
        return res;
    }
}
