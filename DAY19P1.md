# Find Latest Group of Size M
---
- ## Question:
> Given an array arr that represents a permutation of numbers from 1 to n.
> 
> You have a binary string of size n that initially has all its bits set to zero. At each step i (assuming both the binary string and arr are 1-indexed) from 1 to n, the bit at position arr[i] is set to 1.
> 
> You are also given an integer m. Find the latest step at which there exists a group of ones of length m. A group of ones is a contiguous substring of 1's such that it cannot be extended in either direction.
> 
> Return the latest step at which there exists a group of ones of length exactly m. If no such group exists, return -1.
---
- ## Example:
> Input: arr = [3,5,1,2,4], m = 1
> 
> Output: 4
> 
> Explanation: 
> 
> Step 1: "00100", groups: ["1"]
> 
> Step 2: "00101", groups: ["1", "1"]
> 
> Step 3: "10101", groups: ["1", "1", "1"]
> 
> Step 4: "11101", groups: ["111", "1"]
> 
> Step 5: "11111", groups: ["11111"]
> 
> The latest step at which there exists a group of size 1 is step 4.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int findLatestStep(int[] arr, int m) {
        int n = arr.length;
        if (m == n) return n;
        int step = -1;
        int[] map = new int[n + 1];
        int countOfM = 0;
        for (int i = 0; i < arr.length; i++) {
            int current = arr[i];
            int count = 1;
            int leftSpan = 0;
            int rightSpan = 0;
			// If the left side is not 0
            if (current - 1 > 0 && map[current - 1] != 0) {
				// count how many 1s does left side have
                leftSpan = map[current - 1];
				// cause we connect left and right side. 
                if (leftSpan == m) {
                    countOfM--;
                }
				// modify our count of 1s
                count += leftSpan;
				// update the left side
                map[current - 1] = 0;
                
            }
            if (current + 1 <= n && map[current + 1] != 0) {
                rightSpan = map[current + 1];
                if (rightSpan == m) {
                    countOfM--;
                }
                count += rightSpan;
                map[current + 1] = 0;
            }
            
            map[current - leftSpan] = count;
            map[current + rightSpan] = count;
            if (count == m) countOfM++;
            if (countOfM > 0) step = i + 1;
        }
        return step;
    }
}
