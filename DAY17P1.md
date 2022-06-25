# Maximum Value at a Given Index in a Bounded Array
---
- ## Question:
>You are given three positive integers: n, index, and maxSum. You want to construct an array nums (0-indexed) that satisfies the following conditions:
>- nums.length == n
>- nums[i] is a positive integer where 0 <= i < n.
>- abs(nums[i] - nums[i+1]) <= 1 where 0 <= i < n-1.
>- The sum of all the elements of nums does not exceed maxSum.
>- nums[index] is maximized.
>Return nums[index] of the constructed array.
>Note that abs(x) equals x if x >= 0, and -x otherwise.
---
- ## Example:
>Input: n = 4, index = 2,  maxSum = 6
>
>Output: 2
>
>Explanation: nums = [1,2,2,1] is one array that satisfies all the conditions.
>There are no arrays that satisfy all the conditions and have nums[2] == 3, so 2 is the maximum nums[2].
---
- ## Solution:
**Code :**
```java
class Solution {
    public int maxValue(int n, int index, int maxSum) {
        long lo=1 , hi = Integer.MAX_VALUE , result=0;
        
        while(lo<=hi){
            
            long mid= lo + (hi-lo)/2;
            
            long left=Sum(Math.min(index,mid-1),mid); //  here using 0 not 4 as number of element in left  sum will handle that negative part array will look like [0,0,0,0,1,2]. if i choose number of element is left as 4 array will look like [-3,-2,-1,0,1,2]
            left+=Math.max(0,index-mid+1);  //[1,1,1,1,1,2] to make these zeroes one
            
            long right=Sum(Math.min(n-index-1,mid-1),mid);
            right+=Math.max(0,(n-index-mid));
                
            if(left+right+mid<=maxSum){
                result=mid;  //mid is valid but not sure its the maximum answer or not . so lo=mid+1 in next step
                lo=mid+1;
            }else{
                hi=mid-1;
            }    
        }
        
        return (int)result;
    }
    
   private long Sum(long noofElement,long x){
        return x*(noofElement) - ((noofElement*(noofElement+1))/2);
    }
}
