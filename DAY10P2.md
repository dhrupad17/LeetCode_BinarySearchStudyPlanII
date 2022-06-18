# Ways to Split Array Into Three Subarrays
---
- ## Question:
>A split of an integer array is good if:
>
>- The array is split into three non-empty contiguous subarrays - named left, mid, right respectively from left to right.
>
>- The sum of the elements in left is less than or equal to the sum of the elements in mid, and the sum of the elements in mid is less than or equal to the sum of the elements in right.
>
>Given nums, an array of non-negative integers, return the number of good ways to split nums. As the number may be too large, return it modulo 109 + 7.
---
- ## Example:
>Input: nums = [1,1,1]
>
>Output: 1
>
>Explanation: The only good way to split nums is [1] [1] [1].
---
- ## Solution:
**Code :**
```java
class Solution {
    public int waysToSplit(int[] nums) {
        int size = nums.length;
        for (int i = 1; i < size; ++i) {
            nums[i] += nums[i - 1];
        }
        int res = 0;
        int mod = 1_000_000_007;
        for (int i = 0; i < size - 2; ++i) {
            int left = searchLeft(nums, i, size - 1);
            int right = searchRight(nums, i, size - 1);
            if (left == -1 || right == -1) {
                continue;
            }
            res = (res + right - left + 1) % mod;
        }
        return res;
    }
    
    private int searchLeft(int[] nums, int left, int right) {
        int pos = -1;
        int min = nums[left];
        int lo = left + 1, hi = right - 1;
        while (lo <= hi) {
            int mi = lo + (hi - lo) / 2;
            int mid = nums[mi] - min;
            int max = nums[right] - nums[mi];
            if (mid < min) {
                lo = mi + 1;
            } else if (max < mid){
                hi = mi - 1;
            } else {
                pos = mi;
                hi = mi - 1;
            }
        }
        return pos;
    }
    
    private int searchRight(int[] nums, int left, int right) {
        int pos = -1;
        int min = nums[left];
        int lo = left + 1, hi = right - 1;
        while (lo <= hi) {
            int mi = lo + (hi - lo) / 2;
            int mid = nums[mi] - min;
            int max = nums[right] - nums[mi];
            if (mid < min) {
                lo = mi + 1;
            } else if (max < mid){
                hi = mi - 1;
            } else {
                pos = mi;
                lo = mi + 1;
            }
        }
        return pos;
    }
    
}
