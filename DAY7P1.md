# Minimum Number of Days to Make m Bouquets
---
- ## Question
---
>You are given an integer array bloomDay, an integer m and an integer k
>
>You want to make m bouquets. To make a bouquet, you need to use k adjacent flowers from the garden.
>
>The garden consists of n flowers, the ith flower will bloom in the bloomDay[i] and then can be used in exactly one bouquet.
>
>Return the minimum number of days you need to wait to be able to make m bouquets from the garden. If it is impossible to make m bouquets return -1.
---
- ## Example
---
>Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
>
>Output: 3
>
>Explanation: Let us see what happened in the first three days. x means flower bloomed and _ means flower did not bloom in the garden.
We need 3 bouquets each should contain 1 flower.

>- After day 1: [x, _, _, _, _]   // we can only make one bouquet.
>- After day 2: [x, _, _, _, x]   // we can only make two bouquets.
>- After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) {
        int n = bloomDay.length,l = 0, r = findmax(bloomDay); 
        if ((m*k)>n) return -1;
        while (l < r) {
            int mid = l+(r - l) / 2, count = 0, total = 0;
            for (int i : bloomDay){
                if(i>mid) count = 0;
                else if (++count>= k) {
                        total++; 
                        count = 0;
                    }
                
            }
                        
            if (total < m)  l = mid + 1; 
            else  r = mid;
            
        }
        return l;
    }
        private int findmax(int[] A){
        int max=0;
        for (int i :A){
            if (i>max) max = i;
        }
        return max;
        }
    }       
