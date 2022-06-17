# Minimum Absolute Sum Difference
---
- ## Question
---
>You are given two positive integer arrays nums1 and nums2, both of length n.
>
>The absolute sum difference of arrays nums1 and nums2 is defined as the sum of |nums1[i] - nums2[i]| for each 0 <= i < n (0-indexed).
>
>You can replace at most one element of nums1 with any other element in nums1 to minimize the absolute sum difference.
>
>Return the minimum absolute sum difference after replacing at most one element in the array nums1. Since the answer may be large, return it modulo 109 + 7.
>
>|x| is defined as:
>
>- x if x >= 0, or
>- -x if x < 0.
---
- ## Example
---
>Input: nums1 = [1,7,5], nums2 = [2,3,5]
>
>Output: 3
>
>Explanation: There are two possible optimal solutions:
>
>- Replace the second element with the first: [1,7,5] => [1,1,5], or
>
>- Replace the second element with the third: [1,7,5] => [1,5,5].
>
>Both will yield an absolute sum difference of |1-2| + (|1-3| or |5-3|) + |5-5| = 3.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int minAbsoluteSumDiff(int[] nums1, int[] nums2) {
        int[] tempNum  = nums1.clone();
        Arrays.sort( tempNum );
        long totalDiff = 0;
        
        for( int i = 0 ; i < nums1.length; i++ )
            totalDiff += Math.abs( nums1[i]-nums2[i] );
        
        long result = totalDiff;
        for( int i= 0; i < nums2.length; i++ )
        {
            int index = find_index( tempNum, nums2[i]);
            
            int leftIndex = index == 0 ? index : index-1;
            int rightIndex = index == tempNum.length ? index-1 : index;
            
            int diff = Math.min( Math.abs( nums2[i] - tempNum[leftIndex] ), Math.abs( nums2[i] - tempNum[rightIndex] ) );
            
            result = Math.min( result, totalDiff-Math.abs(nums1[i] -nums2[i] ) + diff);
           
        }
    return (int) ( result % 1000000007);    
    }
    
    public int find_index(int[] arr, int K)
    {

        int left = 0;
        int right = arr.length-1;
        while (left < right)
        {
            int mid = (left + right) / 2;
            
            if (arr[mid] == K)
                return mid;
            else if (arr[mid] > K)
                right = mid;
            else
                left = mid + 1;
        }

        return left;
    }
}
