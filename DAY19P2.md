# Sell Diminishing-Valued Colored Balls
---
- ## Question:
> You have an inventory of different colored balls, and there is a customer that wants orders balls of any color.
> 
> The customer weirdly values the colored balls. Each colored ball's value is the number of balls of that color you currently have in your inventory. For example, if you own 6 yellow balls, the customer would pay 6 for the first yellow ball. After the transaction, there are only 5 yellow balls left, so the next yellow ball is then valued at 5 (i.e., the value of the balls decreases as you sell more to the customer).
> 
> You are given an integer array, inventory, where inventory[i] represents the number of balls of the ith color that you initially own. You are also given an integer orders, which represents the total number of balls that the customer wants. You can sell the balls in any order.
> 
> Return the maximum total value that you can attain after selling orders colored balls. As the answer may be too large, return it modulo 109 + 7.
---
- ## Example:
![alt text](https://assets.leetcode.com/uploads/2020/11/05/jj.gif)
> Input: inventory = [2,5], orders = 4
> 
> Output: 14
> 
> Explanation: Sell the 1st color 1 time (2) and the 2nd color 3 times (5 + 4 + 3).
> The maximum total value is 2 + 5 + 4 + 3 = 14.
---
- ## Solution:
**Code :**
```java
class Solution {
   public int maxProfit(int[] inventory, int orders) {
        int lo = 1, hi = Arrays.stream(inventory).max().getAsInt();
        Arrays.sort(inventory);

        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;
            if (getCount(inventory, mid) < orders)
                hi = mid - 1;
            else
                lo = mid;
        }

        int minPrice = lo, ordered = 0;
        long profit = 0;

        for (int i = inventory.length - 1; i >= 0; i--) {
            int curPrice = inventory[i];
            if (curPrice <= minPrice) break;
            profit += (long) (curPrice + minPrice + 1) * (curPrice - minPrice) / 2;
            ordered += curPrice - minPrice;
        }

        profit += (long) minPrice * (orders - ordered);
        profit = profit % 1000000007;
        return (int) profit;
    }

    private long getCount(int[] inventory, int mid) {
        long count = 0;
        for (int i = inventory.length - 1; i >= 0; i--) {
            if (inventory[i] < mid) break;
            count += inventory[i] - mid + 1;
        }
        return count;
    }
}
