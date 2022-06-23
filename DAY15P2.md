# Number of Subsequences That Satisfy the Given Sum Condition
---
- ## Question:
>You are given an array of integers nums and an integer target.
>
>Return the number of non-empty subsequences of nums such that the sum of the minimum and maximum element on it is less or equal to target. Since the answer may be too large, return it modulo 109 + 7.
---
- ## Example:
>Input: nums = [3,5,6,7], target = 9
>
>Output: 4
>
>Explanation: There are 4 subsequences that satisfy the condition.
>
>[3] -> Min value + max value <= target (3 + 3 <= 9)
>
>[3,5] -> (3 + 5 <= 9)
>
>[3,5,6] -> (3 + 6 <= 9)
>
>[3,6] -> (3 + 6 <= 9)
---
- ## Solution:
**Code :**
```java
class Solution {
     public int numSubseq(int[] A, int target) {
        Arrays.sort(A);
        int res = 0, n = A.length, l = 0, r = n - 1, mod = (int)1e9 + 7;
        int[] pows = new int[n];
        pows[0] = 1;
        for (int i = 1 ; i < n ; ++i)
            pows[i] = pows[i - 1] * 2 % mod;
        while (l <= r) {
            if (A[l] + A[r] > target) {
                r--;
            } else {
                res = (res + pows[r - l++]) % mod;
            }
        }
        return res;
    }
}
