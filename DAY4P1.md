# Koko Eating Bananas
---
- ## Question
---
> Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.
>
> Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.
>
> Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.
>
> Return the minimum integer k such that she can eat all the bananas within h hours.
- ## Example
---
>Input: piles = [3,6,7,11], h = 8
>
>Output: 4
---
- ## Solution:
**Code :**
```java
class Solution {
    public int minEatingSpeed(int[] piles, int H) {
        int low = 1, high = 1000000000, k = 0;
        while (low <= high) {
            k = (low + high) / 2;
            int h = 0;
            for (int i = 0; i < piles.length; i ++) 
                h += Math.ceil(1.0 * piles[i] / k);
            if (h > H)
                low = k + 1;
            else
                high = k - 1;
        }
        return low;
    }
}
