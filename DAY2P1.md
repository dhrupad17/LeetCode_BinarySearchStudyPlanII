# Find K Closest Elements
---
- ## Question
>Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.
>
>An integer a is closer to x than an integer b if:
- |a - x| < |b - x|, or
- |a - x| == |b - x| and a < b
---
- ## Example 
>Input: arr = [1,2,3,4,5], k = 4, x = 3
>
>Output: [1,2,3,4]
---
- ## Solution:
**Code :**
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> list= new ArrayList<Integer>(); 
        int low=0;
        int high=arr.length-1;
        while(high-low>=k)
        {
            int dlow=Math.abs(arr[low]-x);
            int dhigh=Math.abs(arr[high]-x);
            if(dlow<=dhigh)
                high--;
            else
                low++;
        }
        while(low<=high)
        {
            list.add(arr[low++]);
        }
        return list;
    }
}
